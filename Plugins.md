# How to do it #

Checkout this project http://code.google.com/p/heeksart/

Change all the occurences of "HeeksArt" to your own project name ( including in the names of files and in the Makefile or .vcproj file ).

Make you own bitmaps and icons.

See how they are used;

Look for occurences of OnSimpleMesh to see how menu and toolbar items are added.

See how to make your own object by copying the CMesh class.
See how it gets its icon in the CMesh::GetIcon method.

Change it until it does what you want it to do.

# Adding it to HeeksCAD #

Start HeeksCAD.

On the File menu, click on "Plugins".

Add a new plugin ( give it a name ) and browse for the ".dll" file ( Windows ) or ".so" file that you build for your plugin.

OK the plugin dialog.

Close HeeksCAD. This adds this plugin text to the HeeksCAD registry entry.

Start HeeksCAD again.

You should see you menu and toolbar!

If HeeksCAD code changes you must build your dll again.

The only way I know to remove the plugin, if HeeksCAD wont run, is to go to the HeeksCAD registry key and delete it or the relevant part. Or for Linux delete the ".HeeksCAD" file in your home directory ( Show Hidden file to see it ).