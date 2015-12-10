.. _geometry-tessellation:

Geometry and Tessellation Shaders
=================================

Remember to look at the :ref:`opengl-pipeline`.

But, just in case, here is the final diagram of the OpenGL pipeline in version 4 and greater:

.. image:: /img/geometry-tessellation/final-pipeline.png

Most of the elements in the pipeline have already been described:

- :ref:`vertex-shader`;
- :ref:`primitive-assembly`;
- :ref:`clipping`;
- :ref:`rasterization`; and
- :ref:`fragment-shader`.

Tessellation Shaders
--------------------

There are two shaders: ``Control`` and ``Evaluation``.

They both operate on a new type of primitive: ``GL_PATCHES``. A patch is just a list of vertices which preserves their order of specification.

They will give errors if patches are not passed to them.

Tessellation Control Shader
^^^^^^^^^^^^^^^^^^^^^^^^^^^

They do the following:

- Generate output patch vertices to be passed to Evaluation Shader; and
- Update per-vertex or per-patch attributes as requires.

Commonly this is a pass-through shader as if often not needed.

Tessellation Evaluation Shader
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

They do the following:

- Executed once for each tessellation coordinate that the primitive generator emits; and
- Sets the position of the vertices derived from the tessellation coordinates.

Geometry Shaders
----------------

Geometry shaders execute once for each primitive (e.g. point, line, or triangle), and they have access to all vertices in the primitive.

They can:

- Add or remove vertices from a mesh;
  - Cull triangles based on some visibility criteria; or
  - Change triangles to points or lines or viceversa; or
  - Shrink triangles; or
  - Emit vertices as components of particle animations.
- Generate geometry procedurally; and
- Add (limited) detail to existing meshes.

This is the last shader to run before the rasteriser.

Although they can add some detail to existing meshes, they are not ideal for general-purpose detail-adding algorithms, because they only have access to surrounding vertices, and not entire polygons.

Main functionality is provided by ``EmitVertex()`` and ``EndPrimitive()``.

This is what a pass-through geometry shader would look like:

.. code-block:: glsl

  #version 400
  layout(triangles) in;
  layout(triangle_strip, max_vertices = 3) out;

  void main()
  {
     for (int i = 0; i<gl_in.length(); i++)
     {
        gl_Position = gl_in[i].gl_Position;
        EmitVertex();
     }

     EndPrimitive();
  }

Compute Shaders
---------------

These are like a stripped-down version of CUDA, and can be used for non-graphics processing that uses the graphics card.

This is interesting because graphics cards tend to be faster and have extra dedicated memory.

But they can mix in with graphics programs (so some of the application computation can be done in the compute shader, while other shaders are also doing their stuff in the graphics pipeline).
