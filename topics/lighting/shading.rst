.. _shading:

Shading
=======

Shading is applying lighting effects in OpenGL code. The three ways below are in increasing realism, but also each take a higher performance hit.

.. contents::
   :local:
   :backlinks: none

In summary, it's something like this:

.. image:: /img/lighting/flat-gouraud-phong.png

Flat Shading
------------

Define a normal for each plane (a.k.a. polygon) that makes up your shape.
Then, calculate lighting for each plane.

This will give you **flat shading**, as shown in the image below.

.. image:: /img/lighting/flat.png

Gouraud Shading
---------------

Define normals at each vertex and use them to calculate lighting

Because the lighting gets calculated at a vertex level, you will see specular highlights appear and disappear quickly.
However, it is cheaper to do than Phong shading (although Phong is acceptably cheap with modern hardware).

.. image:: /img/lighting/gouraud-animation.gif

Below, we can see how the specular highlight follows the vertices as opposed to being truly smooth.

.. image:: /img/lighting/gouraud.png

Phong Shading
-------------

In Phong shading, the normals are defined at vertex level but lighting is not calculated at vertex level.

Instead, the normals are interpolated between vertices, and lighting is calculated at a per-pixel-fragment level.

This means more calculations, and thus it more computationally expensive, but the results are substantially more realistic, and it is more likely to capture specular highlights.

.. image:: /img/lighting/phong.png

Comparison of shading and normals
---------------------------------

Please see original post `here <http://cg2010studio.com/2011/11/01/flat、gouraud、phong-shading的差別-comparison-flat-gouraud-phong-shading/>`_ (in Chinese).

The image below summarises the three main shading models, and also includes bump mapping (which we will look at later on).

.. image:: /img/lighting/comparison.png
