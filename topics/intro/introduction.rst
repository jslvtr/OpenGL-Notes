.. _introduction:

Introduction to this document
=============================


What are graphics?
------------------

Simply **visual images or designs** on a medium, with the purpose to inform, illustrate, or entertain. **Computer graphics** are these on a computer screen.

What is covered in this document?
---------------------------------

This document is mostly taken from `Iain Martin <http://www.computing.dundee.ac.uk/about/staff/17>`_'s Graphics module from The University of Dundee.

It covers OpenGL 4.x, but it is not specifically an "OpenGL module". It is simply a Graphics module, which contains some OpenGL and theory of graphics.

There are a lot of programming examples, and some mathematics is necessary.

Recommended resources
---------------------

Other resources that you may want to look at are:

- "The OpenGL Programming Guide" (latest edition, 8th at time of writing)
- "OpenGL SuperBible" (6th edition at time of writing)
- Books on OpenGL shaders, GLSL (|GLSL|)
- `Anton's OpenGL 4 Tutorials <http://www.amazon.co.uk/gp/product/B00LAMQYF2/>`_

Online resources
^^^^^^^^^^^^^^^^

- `Lighthouse tutorials <http://www.lighthouse3d.com/tutorials/>`_
- `OpenGL resources <https://www.opengl.org/resources/>`_
- `GLFW <http://www.glfw.org/documentation.html>`_

Mathematics
-----------

Although we use libraries and built-in functions where possible, and seldom have to implement our own, it is useful to know some of the mathematics behind it. It's not hard, promise!

- Vectors (dot product, cross product)
- Matrices (and operations with them)
- Simple geometry (lines, planes, 3D geometry like spheres)
- Trigonometry
- Fractals and Noise functions (towards the end)

Why OpenGL?
-----------

The first vendor-independent API for development of graphics applications.

There is no need to license it to use it.

It was designed to use the graphics card where possible to improve performance.

Originally based on a state machine, procedural model; thus it can be used with a wide variety of programming languages (using Python in this document).

Primitives
^^^^^^^^^^

OpenGL is platform independent, but does utilize hardware natively. We define our models using OpenGL primitives (vectors and matrices, mostly). OpenGL passes this to the hardware.

GLSL (|GLSL|) allows (normally small chunks of) code to run in the graphics hardware. This code executes **substantially** faster than if it were executed in the CPU, as would happen in *normal* programming.

OpenGL versions
---------------

At time of writing, OpenGL 4.5 is the latest version.
**Mac OS X 10.11 only supports OpenGL 4.1**.

1. OpenGL 1.x
	- Based on a state machine and procedural model
2. OpenGL 2.x
	- Includes shading language (vertex and fragment)
	- Numerous stacked extensions
3. OpenGL 3.3 onwards
	- Forked into compatibility and core directions
	- Geometry shaders (which were actually introduced in 3.2)
4. OpenGL 4.x
	- Updates to shading language (tessellation shaders)
	- Support for embedded devices

.. |GLSL| replace:: "OpenGL Shading Language"