.. _mapping:

Bump and Normal Maps
====================

Bump map
--------

A bump map is a heightmap (a file of gray-scale values, where the height is depicted by a darker gray) used to modify surface height by modifying the normal.

It's about the fine-grained detail of the object rather than the colour.

However it is not very used anymore.

Normal map
----------

Has a similar effect to bump mapping, but the file uses RGB colours instead of a gray-scale. It is generally considered superior to bump-mapping.

It is a complex topic, but a tutorial is available `here <http://www.opengl-tutorial.org/intermediate-tutorials/tutorial-13-normal-mapping/>`_.

Displacement mapping
--------------------

This is, in contrast to the two above, not a "fake" technique.

This technique is used to actually modify the geometry of the shape to which it is applied, and this can be done in the tessellation shaders.

It is used to add high-resolution mesh detail to a low-resolution mesh.
