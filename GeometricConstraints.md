# Introduction #

HeeksCAD has a built in geometric constraints solver. Allowing you to make inaccurate sketches into perfect drawings.


# Details #

First, there are a couple of options that make things a whole lot easier. In the options panel:

Go to digitizing, and turn on autosolve constraints.
Go to selection filter, and turn off sketches.

Now, you can use the line arc drawing tool to make a polygon. Pressing and holding 'a' while drawing allows you to insert an arc segment.

After drawing, you can select a segment by clicking on it. Dragging the points will move the edges of the polygon around. A right click brings up a context menu allowing you to add/remove constraints. The items in the context menu will change depending on what is selected. Ctrl clicking allows multiple things to be selected.

1 line selected:
> horizontal,vertical,length
2 lines selected:
> parallel,perpendicular,colinear,equal length
1 arc selected:
> radius
2 arcs selected:
> concentric,equal radius
1 arc and 1 line selected:
> arc tangent to line
2 points selected
> points coincident
1 point and 1 line selected
> point on line, point on midpoint of line
1 point and 1 arc selected
> point on arc, point on midpoint of arc
1 circle and 1 line selected
> circle tangent to arc
2 circles selected
> equal radius and concentric circles
1 circle and 1 arc selected
> equal radius and concentric circle and arc

After setting the parameter based constraints(length or radius), you can now change the parameter in the properties pane. This will update the geometry automatically.

Double click the sketch in the objects panel will put you in "sketch mode". This will cause and new polygons or circles to become part of the existing sketch. Hitting escape twice will exit sketch mode.

# Examples #
To view and example of using a constraint sketch see [this video](http://www.youtube.com/watch?v=nibjuxCbUag)