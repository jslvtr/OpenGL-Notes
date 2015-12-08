.. _texturing:

Texturing
=========

Texturing or texture mapping is extremely important for realism.

Simply it is attaching a picture to a polygon. It can give the impression of materials, like wood or granite.

Each point of the image is called a "texel" in analogy to pixels, and the image coordinates range from ``(0, 0)`` (bottom-left) to ``(1, 1)`` (top-right).

Multi-texturing
---------------

Can bind textures to different OpenGL texture elements. Each also needs a separate texture sampler, for example::

  glActiveTexture(GL_TEXTURE0)  # This is for the first texture element
  glBindTexture(GL_TEXTURE_2D, textureID0)
  glBindSampler(GL_TEXTURE0, textureSamplerID0)

  glActiveTexture(GL_TEXTURE1)  # This is for the second texture element
  glBindTexture(GL_TEXTURE_2D, textureID1)  # And here we bind to it the texture with id textureID1
  glBindSampler(GL_TEXTURE1, textureSamplerID1)

Then, the fragment shader code could look something like this:

.. code-block:: glsl

  in vec4 fcolour;
  in vec2 ftexcoord;
  out vec4 outputColor;

  layout(binding = 0) uniform sampler2D tex1;
  layout(binding = 1) uniform sampler2D tex2;

  void main()
  {
   vec4 texcolour1 = texture(tex1, ftexcoord);
   vec4 texcolour2 = texture(tex2, ftexcoord);
   outputColor = fcolour * (texcolour1 * texcolour2);
  }

Anti-aliasing textures (mipmapping)
-----------------------------------

Mipmapping is creating or providing the same texture at different resolutions, for use when the texture is rendered at a distance.

For example, the same texture could be provided (or calculated) at 64x64, 32x32, 16x16, 8x8, 4x4, 2x2, and 1x1.

Mapping textures to surfaces
----------------------------

Distortion often results, especially if mapping to a sphere, for example.

For simple polygons, mapping the texture can be very simple: just define texture coordinates for each vertex.

For more complicated shapes things can get tricky. Something we can do is shrink-wrap mapping:

.. image:: /img/texturing/shrink-wrapping.png
