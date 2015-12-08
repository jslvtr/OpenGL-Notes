.. _lighting:

Lighting
========

Phong Lighting Model
--------------------

Lighting is based on the Phong model, which states that for every object, we can see light reflected from it in three ways:

- Ambient light;
- Diffuse reflection; and
- Specular reflection.

.. image:: /img/lighting/light-reflections.gif

Ambient light
^^^^^^^^^^^^^

Usually light gets reflected from surfaces and walls, so entire scenes have a small amount of light even when they
are not pointing towards the light source.

We can model that (unrealistically) using ambient light: giving the entire scene a small amount of light that is applied to all objects.

This is not realistic, but does a reasonably good job and does not entail a performance loss.

Diffuse reflection
^^^^^^^^^^^^^^^^^^

This is light that gets reflected in all directions when a light ray hits a surface.

When the surface is parallel to the ray of light, it does not get hit, and so no diffusion can take place.

When the surface is perpendicular to the ray, maximum diffusion takes place. This follows **Lambert's Law** [#f1]_:

.. math::
  :nowrap:

  R_d = I_dK_dcos(\theta) = I_dK_d(N.L)

Where:

- :math:`I_d` is the intensity of the incoming light ray.
- :math:`\theta` is the angle between the light and the surface normal.
- :math:`K_d` is the diffusion constant, the "non-glossyness" of the surface.
- :math:`N` is the surface normal vector.
- :math:`L` is the direction of the light coming from the light source.

Specular reflection
^^^^^^^^^^^^^^^^^^^

A **Specular Highlight** is the reflection we see when the angle of incidence equals the angle of reflection, and our eye is in position at that angle to see the reflection.

For a perfectly glossy surface, the specular highlight can only be seen for a small :math:`\theta`, as in below:

.. image:: /img/lighting/specular.png

However, for a non-glossy surface, there is a range of :math:`\phi` where the specular highlight can be seen.

The equation is as follows:

.. math::
  :nowrap:

  R_s = I_sK_scos^{n}(\theta)

Phong suggested a large value of :math:`n` for a large range of :math:`\phi`, and a small value of :math:`n` for a small range.

Blinn-Phong approximation
~~~~~~~~~~~~~~~~~~~~~~~~~

The Blinn-Phong approximation is used in OpenGL as a means to simulate the equation but made simpler.

.. image:: /img/lighting/specular-approximation.png

Instead of using the angle betwee :math:`R` and :math:`V`, we calculate :math:`S` which is between :math:`L` and :math:`V`.
Then, we use the angle between :math:`S` and :math:`N`.

Emitted light
^^^^^^^^^^^^^

An object can emmit light, and this simply means that we program it to be bright, as if it were a source of light.

Attenuation
^^^^^^^^^^^

The intensity of the light must decrease the further away from the light we are, unless the light is directional, and not positional.

Although light intensity can be calculated with a number of formulas (e.g. the square of the distance from the light), we can use a more complex formula when programming graphics:

.. math::
  :nowrap:

  1\over{k_c+k_{l}d+k_{q}d^2}

Where :math:`k_c`, :math:`k_l`, and :math:`k_q` are constants, and :math:`d` is the distance from the light for any given position.

.. rubric:: Footnotes

.. [#f1] Lambert's Law states that the intensity of the diffused light is proportional to the cosine of the angle between two vectors, the surface normal and the direction of the light source.
