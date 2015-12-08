.. _transformations:

Transformations
===============

Every object has a matrix associated with it, so that we can easily apply transformations to it and pass it to the shader to determine the correct position of the object.

Before applying any transformations, an object must have the identity matrix associated with it.

This matrix does not apply any transformations. When a matrix is multiplied by the identity matrix, the result is the original matrix. The identity matrix looks like this:

.. math::
   :nowrap:

	\begin{bmatrix}
	1&0&0&0\\
	0&1&0&0\\
	0&0&1&0\\
	0&0&0&1
	\end{bmatrix}

Multiplying the identity matrix by another matrix results in the matrix being returned:

.. math::
   :nowrap:

   \begin{bmatrix}
   1&0&0&0\\
   0&1&0&0\\
   0&0&1&0\\
   0&0&0&1
   \end{bmatrix} .
   \begin{bmatrix}
   3&2&0&1\\
   4&2&2&0\\
   4&1&3&0\\
   0&2&2&2
   \end{bmatrix} =
   \begin{bmatrix}
   3&2&0&1\\
   4&2&2&0\\
   4&1&3&0\\
   0&2&2&2
   \end{bmatrix}

Simple transformations
----------------------

Translation
^^^^^^^^^^^

A translation matrix looks like this:

.. math::
   :nowrap:

	\begin{bmatrix}
	1&0&0&T_x\\
	0&1&0&T_y\\
	0&0&1&T_z\\
	0&0&0&1
	\end{bmatrix}

We can multiply a position vector by a translation matrix and see that we end with a translated vector:


.. math::
  :nowrap:

  \begin{bmatrix}
  1&0&0&5\\
  0&1&0&1\\
  0&0&1&1\\
  0&0&0&1
  \end{bmatrix} .
  \begin{bmatrix}
  3\\
  5\\
  2\\
  1
  \end{bmatrix} =
  \begin{bmatrix}
  1*3+5*1\\
  1*5+1*1\\
  1*2+1*1\\
  1
  \end{bmatrix} =
  \begin{bmatrix}
  8\\
  6\\
  3\\
  1
  \end{bmatrix}

Rotation
^^^^^^^^

A rotation matrix rotates a vertex around a line by :math:`\theta` degrees.

A matrix to rotate a vertex around the ``x`` axis:

.. math::
   :nowrap:

	\begin{bmatrix}
	1&0&0&0\\
	0&cos(\theta)&-sin(\theta)&0\\
	0&sin(\theta)&cos(\theta)&0\\
	0&0&0&1
	\end{bmatrix}

A matrix to rotate a vertex around the ``y`` axis:

.. math::
  :nowrap:

	\begin{bmatrix}
	cos(\theta)&0&sin(\theta)&0\\
	0&1&0&0\\
	-sin(\theta)&0&cos(\theta)&0\\
	0&0&0&1
	\end{bmatrix}

A matrix to rotate a vertex around the ``z`` axis:

.. math::
  :nowrap:

	\begin{bmatrix}
  cos(\theta)&-sin(\theta)&0&0\\
	sin(\theta)&cos(\theta)&0&0\\
  0&0&1&0\\
	0&0&0&1
	\end{bmatrix}

Scaling
^^^^^^^

A scaling matrix will multiply the vertices to expand or reduce the size of a polygon.
The matrix below, if applied to a group of vertices making a polygon, would expand the polygon by a factor of 3.

.. math::
   :nowrap:

	\begin{bmatrix}
	3&0&0&0\\
	0&3&0&0\\
	0&0&3&0\\
	0&0&0&1
	\end{bmatrix}

Combining transformations
-------------------------

We can combine transformations, such as scaling an object and then rotating it.
Remember that the order in which we apply transformations does matter.

For example, if we have an object at position ``(0, 0, 0)`` (the origin), and we rotate it around the origin, it will rotate in place. Then we can move the rotated object elsewhere.

However, if we first move the object and then rotate it around the origin, the object won't rotate around itself, it will in fact move.

If we want to combine transformations, **we much apply transformations in reverse order to which we want them to happen**.

If we wanted to first rotate and object and then scale it, this would be the order to do it in:

.. math::
  scale * rotate * objectmatrix

So the matrices would look something like this (scaling by 3 and rotating by 45°):

.. math::
  :nowrap:

  \begin{bmatrix}
	3&0&0&0\\
	0&3&0&0\\
	0&0&3&0\\
	0&0&0&1
	\end{bmatrix} .
  \begin{bmatrix}
	1&0&0&0\\
	0&cos(45)&-sin(45)&0\\
	0&sin(45)&cos(45)&0\\
	0&0&0&1
	\end{bmatrix} .
  \begin{bmatrix}
	1&0&0&0\\
	0&1&0&0\\
	0&0&1&0\\
	0&0&0&1
	\end{bmatrix}

And this would give you the model matrix for your object:

.. math::
  :nowrap:

  \begin{bmatrix}
	3&0&0&0\\
	0&2.12&0&0\\
	0&0&2.12&0\\
	0&0&0&1
	\end{bmatrix}
