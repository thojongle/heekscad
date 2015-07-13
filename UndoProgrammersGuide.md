# Introduction #

HeeksCAD has a smart and automatic undo/redo engine designed to relieve programmer pain and reduce bugs. This means for the most part you don't need to do anything to have your code work with undo/redo. This document is therefore mostly for people adding new UI methods or new HeeksObj's. People writing just algorithms that work on the tree and its elements probably do not need to read this. Although it may be helpful or enlightening to know what is going on under the hood.


# UI Methods #

Currently all UI for algorithms is done via buttons or menu items, this is unlikely to change, but it might. Whenever a button or menu item is clicked, heekscad looks up what code to run. Before running it, it calls CreateUndoPoint(). This function analyzes the tree for any changes and stores the relevant information for undoing/redoing it later. Then the algorithm itself is called. Finally, Changed() is called to force an update of the treeview.

So in code, the process is this

OnButton()
{
> CreateUndoPoint();
> tool->Run();
> Changed();
}

These methods are part of HeeksCADapp and are accessible by either wxGetApp() or the application pointer in a plugin. If you are experiencing weird things like new objects not being put in the treeview, extra undo points, or your changes being grouped in with other changes, it is best to set a breakpoint in your algorithm at look at the call stack. No more than 3 calls above you should see code that look substantially like the above. If not, find a good place to put it, keeping in mind your algorithm is not a good place for the undo code. Only code that explicitly deals with a UI event should call undo. Later on someone may use you algorithm as part of some large scripted sequence and the individual parts of that algorithm should not be undoable.

# Heeks Objects, the simple kind #

When creating a new class that inherits directly or indirectly from HeeksObj, there are a couple methods which must be implemented correctly for undo to work properly, and a couple more that may be required to make it work well depending on the case.

**MakeACopy**

This is a pure virtual function of HeeksObj, so normally the compiler will barf if it is not implemented. But, in cases of multiple inheritance, the base class often implements this, so the compiler will not complain, and your code just won't work.

Make sure it is implemented like this example:

HeeksObj `*`HLine::MakeACopy(void)const{
> HLine `*`new\_object = new HLine(`*`this);
> return new\_object;
}

Notice the `*`this. I've found a couple of cases where the `*` was omitted, which compiled because there was a constructor taking a HLine`*`, but did not work as the = operator is not called in this case.

**= Operator**

This operator must be implemented for your class to work properly. Do not count on a base class implementing. Here is an example:

const HLine& HLine::operator=(const HLine &b){
> EndedObject::operator=(b);
> color = b.color;
> return `*`this;
}

Notice the calling of the base classes = operator, this is imperative, even if just inheriting from HeeksObj. All state variables declared by the class must be copied. Do not copy any base classes members.

**IsDifferent**

This method tells the undo engine if an object has been modified. This method will only be called if the object in question is known to be of the same type, has the same id, and is the same place in the tree.

All state variables declared by this class should be checked for equality, If not return true. The base classes IsDifferent should be returned if the objects appear to be equal. Here is an example:

bool EndedObject::IsDifferent(HeeksObj `*`other)
{
> EndedObject`*` eobj = (EndedObject`*`)other;
> if(eobj->A->m\_p.Distance(A->m\_p) > wxGetApp().m\_geom\_tol)
> > return true;


> if(eobj->B->m\_p.Distance(B->m\_p) > wxGetApp().m\_geom\_tol)
> > return true;


> return HeeksObj::IsDifferent(other);
}

**ReloadPointers**

Some objects have pointers to there child objects as members. I'm calling these quick pointers. For example, HLine has a pointer A and B to HPoints. These points are also children of HLine. There will be times when the undo engine decides to modify the children, making A and B invalid. If your object uses quick pointers it should implement ReloadPointers(), it must then be able to search the ObjList for A and B and reset its quick pointers. Again, always call the base classes ReloadPointers if you override.

# Heeks Objects, the more complicated kind #

Some HeeksObj's have numerous children that are not particularly related to there state. An example would be a CShape. The state of this object is wholly determined by the TopoDS\_Shape that it contains, yet it has numerous faces, edges, and vertices as children. Not only would searching the faces and edges for changes be time consuming, but replacing them would be pointless as it would not update the TopoDS\_Shape that they represent.

**DescendForUndo**

Implementing this function will prevent the undo engine from examining children. Instead the entire tree, with this node at the top, will be copied whenever IsDifferent returns true.

**IsDifferent**

Analyzing a TopoDS\_Shape or ToolPath for changes would be time consuming and is not necessary. Instead you can use a creation time field. Just initialize this in constructors to the current time and copy it in the = operator. Then use IsDifferent to just check for a difference in creation time. Any operations that regenerate a tool path or some such thing, if they do not create a new object, must update this time.

# Heeks Objects, the really complicated kind #

Some objects in HeeksCAD have multiple parents. The only objects currently doing this are geometric constraints. It is supported if you need or want to do it. The undo engine supports copying subtrees with dangling edges and the reintegration of such graphs into the main tree. This is done by storing the edges of the graph rather than the nodes themselves. That way the appropriate connectivity is known and can be used to setup the graph after a full or partial copy.

**IsTransient**

Implement this and return true if this node has multiple parents, or can in certain situations. This will cause the undo engine to use the edge rather than node analysis. In theory this could be used on all objects, multiparented or not. This code is not as well debugged, probably best to use when needed.