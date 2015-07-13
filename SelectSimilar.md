# Introduction #

If the operator presses the SHIFT key while in 'select' mode and then select a single graphical object, the software will search the rest of the model for other graphical objects that 'look like' that selected.

This 'correlation test' is done both on size and shape.  It has parameters, included beneath the 'correlation' parameter set, that allow the operator to adjust how similar in size and how similar in shape the various objects need to be before including them in the results set.  (Note: If the operator selects a Point as the reference object, the size and shape comparisons are discarded.  Instead, it will select all Point objects in the model)

In the case of HeeksCNC, this CorrelationTool can be used as a source of locations for a drilling cycle operation.

# Details #

This module tests size by comparing the diagonal length of each bounding box.  The reference object's bounding box diagonal length is compared with each other graphics element's bounding box diagonal.  This comparison allows for both smaller and larger scaling based on a configurable parameter.

The second check is to determine shape.  The algorithm is to draw a line from the centre of each object at a configurable number of angles.  These lines are intersected with the object and both the number of intersections and the distance between the intersection and the centre is recorded.  Each distance is scaled based on the scaling test above.  Once this is complete, a score is assigned based both on the number of intersections at each angle and the intersection distance at each angle.  This score is averaged over the number of samples and compared with a configurable parameter.

NOTE: Not all of the underlying graphical elements support the intersection of themselves and the Line objects.  In these cases the objects are selected/rejected based on the size check alone.

# Example Workflow #

I did this with the intent of generating the drilling cycles required to produce a printed circuit board (PCB).

> - Import a raster image of a PCB into Inkscape.

> - Use the edge detection and GCode generation routines to produce both a vector SVG file and the GCode necessary to do the 'isolation routing' operation.

> - Import the SVG file into a HeeksCNC model.

![http://heekscnc.googlecode.com/svn/wiki/CorrelationTool/Wiki_CorrelationTool_pcb_following_edge_detection.png](http://heekscnc.googlecode.com/svn/wiki/CorrelationTool/Wiki_CorrelationTool_pcb_following_edge_detection.png)

> - With the SHIFT key depressed, select one of the circles that surrounds a drill hole.

![http://heekscnc.googlecode.com/svn/wiki/CorrelationTool/Wiki_CorrelationTool_with_drill_bit_made_and_pad_selected.png](http://heekscnc.googlecode.com/svn/wiki/CorrelationTool/Wiki_CorrelationTool_with_drill_bit_made_and_pad_selected.png)

> - Depress the CONTROL key so as to select one more object before selecting a CuttingTool tool to represent the drill bit.

> - Insert a DrillingCycle operation.

![http://heekscnc.googlecode.com/svn/wiki/CorrelationTool/Wiki_CorrelationTool_with_drilling_operations_found.png](http://heekscnc.googlecode.com/svn/wiki/CorrelationTool/Wiki_CorrelationTool_with_drilling_operations_found.png)

> - Adjust the DrillingCycle operation's parameters such as depth etc.