.. _particles:

Particles
=========

Many effects can be simulated by particles: smoke, fire, rain, snow, etc...

Each of the particles could have simple behaviour (like just moving down, or to the side), or they could have more complex movement, like gravity or collisions with other particles.

The best way to implement particle systems in OpenGL is by using instancing:

1. Send a particle object to the pipeline; and
2. Draw different instances of it with one command.

GL_POINTS for particles
-----------------------

It is efficient to use ``GL_POINTS`` to draw your particles, as opposed to other primitives like complex polygons, because it is more efficient as they have no geometry.

It is also easy to modify the final shape of the particle by discarding pixel fragments at the fragment shader stage.

You can control the point size in the shader like so:

.. code-block:: glsl

  gl_PointSize = (1.0 - pos2.z / pos2.w) * size;

It is easy to discard pixel fragments in the fragment shader like so (example below to make a circle from a ``GL_POINT``):

.. code-block:: glsl

  vec2 temp = gl_PointCoord - vec2(0.5);
  float f = dot(temp, temp);
  if (f>0.25) discard;

``gl_PointCoord`` is a variable which contains **where within a point primitive the current fragment is located**, and only works for ``GL_POINTS``.

.. image:: /img/particles-mapping/point-discard.png
