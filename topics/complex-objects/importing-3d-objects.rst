.. _importing-3d-objects:

Importing 3D objects
====================

We can use a package like the following:

- Blender
- 3DS Max
- Autodesk Maya
- Houdini

We will also need a way to load the objects these packages create:

- Assimp
- Load Blender .obj files (essentially text files)
- Lib3ds

Assimp relies on D3D9, so it is not recommended unless you are using windows. Reading in the text files by creating your own object loader is recommended.

.obj files
----------

The .obj file exported from Blender will look something like this::

	# Blender
	o ModelName
	v 0.5 0 1
	v 1.0 0 1
	v 0.6777772 0.5 1
	f 1 2 0
	f 2 0 1
	f 1 0 2

A line starting with ``o`` defines the model name, one starting with ``v`` defines a vertex position, and one starting with ``f`` defines a triangle face from three vertices.