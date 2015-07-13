# Introduction #
'Digitizing' in HeeksCAD refers to the process of specifically locating coordinates in 3d space.  It is desireable to locate points this way for several related operations.

**snapping** as implemented in other applications (where the placement of one object is pulled toward a grid, or other object).  Objects in HeeksCAD are dragged by the control handle and it is this handle which is "snapped" to the target location.

**Transforms**  Multi step operations for moving, scaling, or duplicating objects.  Transforms are often controlled by selecting a reference and target location.

**Drawing new geometry**  Adding sketches or solids to a model where precise placement of points is required.

For all these activities, the options for selecting reference coordinates are found under the digitizing menu.


# Candidate Points #

The following can be used for either reference or target points.  Development is not finished in this area so some selection types don't work for all objects.

| **Option** | **Definition** | **Works with** |
|:-----------|:---------------|:---------------|
| End        | The end point of a line or edge | Line, arc, spline, edge |
|Intersection|The intersecting point of two lines or edges|line, infinite line,circle, arc, ellipse|
|centre      |A point equidistant from all other points in the object|sphere, arc, circle, ellipse|
|midpoint    |A point equidistant between the ends| line, edge     |
|nearest     |The point on an entity closest to the cursor|line, arc, circle, ellipse, spline|
|tangent     | Allows drawing lines and moving objects tangent to other objects |arc, circle, ellipse, infinite line, line, spline|

# Non-point control #

The following options control other aspects of digitizing but do not rely on the existing geometry.

**coordinates** In most cases, it should be left on.  Turning it off constrain the points available to only those that are snapable from the options above.  It will not be possible to draw or drop an object anywhere else.  Attempting to drag an object to empty space will cause it to be moved to the global coordinate system origin.  It can be turned off when drawing a sketch to allow snapping only to endpoints and not the grid or intermediate coordinates.

**screen** This controls whether objects in the plane of the screen.  If the view is set XY and screen is turned on.  A sphere at z=10 is moved over the sketch, the sphere snaps to the end-point with z=radius.  With screen turned off, the sphere is moved to the endpoint with z=endpoint z.


**snap to grid** Snap to the on-screen grid whose size is controlled by the grid size option.  If 'snap to grid' is off, the grid will automatically subdivide by 1/10 as the user zooms in and out.  If 'snap to grid is on, the grid size remains fixed during zooming.  It is not possible to snap-to-grid unless 'coordinates' is also enabled.

# Options #

**grid size**  default: 1.  Controls the size of the onscreen grid.

**autosolve constraints**  Turns on and off the autosolving of constraints. Refer to the GeometricConstraints page.
