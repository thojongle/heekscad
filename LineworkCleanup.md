# Introduction #

There are occasions where sketches representing the model contain many more graphical elements than are required.  For example an SVG file may include spline elements that contain 20 or 30 poles but whose overall length is less than 1mm.  In such situations, the bloated size of the graphical model only serves to slow down the computer's processing.

In such situations, it may be preferable to convert the series of many small graphical elements into fewer, and larger, lines or BSplines.

The 'Simplify Sketch to Lines' and 'Simplify Sketch to BSpline' menu options take each selected sketch in turn.  They interpolate points along all of the sketches elements such that the points are never more than a configurable deviation from the original piece of graphics.

These simplification routines then iterate through these points removing adjacent points where the distance between them is less than the configured tolerance.

The process then steps through the interpolated points in groups of three.  It draws a line between the two outside points (in memory only) and measures the distance of the centre point to this line.  If the deviation from the centre point to the line is less than that configured then the centre point is discarded.

These two point removal processes continue until none of the interpolated points can be discarded without contradicting either the tolerance or the deviation settings.

With this simplified set of interpolated points, the software then generates either a series of lines or a single bspline that intersects all interpolated points.

If a simplified element can be created, the software adds the word 'Replaced ' to the original element's title before adding the newly created element to the Heeks file.  The idea being that the modified title will make the replaced object easier to identify for manual removal.


# Options #

There are a series of options available to help configure the constraints of this process.  Such options can be seen beneath the 'Simplify Sketch Options' within the 'Options' window.

## Max Deviation ##

When the points are being interpolated along the original element's graphics, this is the maximum distance between the interpolated points and the original graphical elements.  Values such as 0.001 (mm) are typical.

## Cleanup Tolerance (temporary) ##

When the original sketch contains many child graphical elements, these elements may or may not be connected to each other.  Normally, such measurements use the 'drawing->geometry tolerance' value to determine if two points are coincident.  For the linework cleanup routines, this 'geometry tolerance' may be replaced with the 'cleanup tolerance' for the purposes of cleanup only.  i.e. the global geometry tolerance is replaced with the cleanup tolerance and the original geometry tolerance reinstated when the cleanup processing is complete.

Changing this value is one way of closing gaps in disjointed sketches so that the resultant sketch will be made up of a single, connected, series of graphics.

## BSpline Min Degree, BSpline Max Degree and BSpline Continuity ##

These three parameters are used when a bspline constructed.  The construction process ensures that the bspline intersects all of the simplified interpolated points.  These three parameters help describe the mathematical equations that govern where the bspline goes between these interpolated points.

Typical values are;  min degree = 3, max degree = 8 and continuity = GeomAbs\_C2

## Sort Points ##

This True/False flag determines whether the list of interpolated points is sorted before being cleaned up.  The idea is to sort the points list such that each point is physically closest to the previous point.  If the graphics doubles back on itself this can, sometimes, improve the result.  Of course there are also geometrical examples where this sorting option produces erroneous results.  Please consider it just one more tool in the set that may help improve the data.

## Force Closed Shape ##

If this flag is true, the application ensures that the last and first points in the interpolated points list are coincident.  If they are not then an extra point is added to the end of the list so that the shape is closed.