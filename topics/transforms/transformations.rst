.. _transformations:

Transformations
===============

Every object has a matrix associated with it, so that we can easily apply transformations to it and pass it to the shader to determine the correct position of the object.

Before applying any transformations, an object must have the identity matrix associated with it.

This matrix does not apply any transformations. When a matrix is multiplied by the identity matrix, the result is the original matrix.

.. math::
   :nowrap:

	\begin{pmatrix}
	1&0&0&0\\
	0&1&0&0\\
	0&0&1&0\\
	0&0&0&1
	\end{pmatrix}