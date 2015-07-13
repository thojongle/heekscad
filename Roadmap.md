# Introduction #

This document outlines the future plans for heekscad. It is currently very much a work in progress. Edits and discussions on forums are encouraged. At some point these things will be converted into issues in bug tracker.

All of the issues in bug tracker need to get taken care of. At the very least they should be inserted into this document under some milestone. Some things may need to be marked as do not fix, others are probably fixed, but there reporters have not verified them as so. Imho, these should be marked as fixed and they will just get rereported if they are not.

It isn't clear to me if we should start milestoning before or after 1.0. The following list is stuff I think needs to happen for 1.0. Earlier stepping stones may be advisable depending on how big this list gets and the inter-dependencies or infrastructure requirements that arise as a consequence.

# 1.0? / M1? #

  1. DXF importer needs support for ~~points and~~  elliptic arcs.
  1. DXF export is seriously behind import.
  1. ~~Add buttons for drawing splines and ellipses~~
  1. Set some kind of maximum undo depth.
  1. Garbage collector for HeeksObj's. Should be tied into the UndoEngine somehow as this is the only way objects ever get deleted.
  1. Ellipses and Elliptic arcs should be different entities
  1. Pretty symbolism for constraints.
  1. Angular dimension object
  1. Multipoly should work for lines arcs and circles at least without crashing
  1. Fix the reordering of objects by UndoEngine
  1. Get rid of flickering and collapse of the tree by Changed()

# M2 #

  1. Need a system for determining the coordinate system of a sketch
  1. Use the above coordinate system to project the mouse cursor onto a plane when editing geometry
  1. System for updating dynamic solids when needed/if possible. Perhaps using another thread to do the updates
  1. OpenGL Tree View
  1. System for determining the associative geometry of a face. For example when a solid has been produce by a number of operations, such as a pad or two, some pockets, and a fillet, we must know that the face is associated with a specific line.

# Wishlist #

  1. Svg export
  1. Linewidth from dxf, linewidth and color from svg
  1. Block and reference objects.
  1. Constraint inference engine. (Infers constraints when loading non native file formats)
  1. Allow transformations by non orthogonal matrices. Start with 2d stuff, then move to 3d