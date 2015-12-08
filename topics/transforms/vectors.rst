.. _vectors:

Vectors
=======

Vectors are simply 2, 3, or 4 dimension elements. In OpenGL we often use them to specify position, direction, velocity, colour, or a lot more.

.. image:: /img/transforms/vector.png

The axes as shown in the image above are the default OpenGL axes. However, it is possible to change them, inverting the Z axes.

Vector operations
-----------------

To add or subtract vectors, simply each of the dimensions together.

The **length** of a vector is given by the equation :math:`|V| = \sqrt{x^2 + y^2 + z^2}`.

To scale a vector (multiply a vector by a scalar), just multiple each of the dimensions by the scalar.

To normalise a vector, divide the vector by its length, like so

.. math:: U = {V\over|V|}

Normal vectors
--------------

Normal vectors can be normalised, but they are not the same thing!

A normal vector specifies the direction which a surface is looking towards.

For example, in a cube you would want the light to shine on the outside of the cube, and not on the inside. What to do is define the normals for each of the vertices of the cube to be facing outwards from the cube. If you made them face inwards, then the cube would be lit on the inside, and would look black on the outside.

.. image:: /img/transforms/normal_vector.png

The image above shows the normal vector for a plane.

Remember that the normal vector is the direction the plane is looking towards. If we change the normal vector without changing the rotation of the plane, the lighting would change, but it may not look physically realistic.

Dot Product of Two Vectors
--------------------------

To calculate the dot product of two vectors, watch the video `here <https://youtu.be/W_CI8KQz0fA>`_.

A more comprehensive explanation of why that works is `here <http://www.mathsisfun.com/algebra/vectors-dot-product.html>`_.

Cross Product of Two Vectors
----------------------------

To calculate the cross product of two vectors, watch the video `here <https://youtu.be/Ix9HGSxlevk>`_.

A more comprehensive explanation of why that works is `here <http://www.mathsisfun.com/algebra/vectors-cross-product.html>`_.

Homogeneous Coordinates
-----------------------

Homogeneous coordinates are just 3D vectors that instead of 3 dimensions have 4 dimensions. Usually the 4-th coordinate is ``1``.

This is used for things like translations (we will see soon), and to define whether a vector is simply a direction (``w == 0``) or a position (``w != 0``).

Thus the vector ``(x, y, z, w)`` corresponds in 3D to ``(x/w, y/w, z/w)``.