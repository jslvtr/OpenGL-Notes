.. _drawing:

Drawing
=======

I recommend `reading this <http://www.labri.fr/perso/nrougier/teaching/opengl/>`_ before continuing.

There are a number of steps in drawing:

.. contents::
   :local:
   :backlinks: none
  
VAO & VBO
---------

When drawing we start with a Vertex Array Object (VAO) and Vertex Buffer Objects (VBOs).

Good information regarding VAO and VBO can be found `here <http://www.swiftless.com/tutorials/opengl4/4-opengl-4-vao.html>`_.

The gist of it is that Vertex Array Object is a really bad name for what that VAO is. It may be better to call it a Vertex Buffer Array, as that tells us more of what it does.

Essentially the VAO holds what data we are going to be sending the OpenGL pipeline. So, usually we need to send the pipeline data like vertices and colours we are drawing, but potentially more stuff as well like textures or normal maps.

Those attributes, like vertices, colours, textures, and more are stored in the Vertex Buffer Object (VBO).

So it goes in this order:

1. Generate Vertex Array Object
2. Bind Vertex Array Object
3. Generate Vertex Buffer Object
4. Bind Vertex Buffer Object

Steps 1 and 2 are as follows::

	glGenVertexArrays(1, &vaoID[0]); // Create our Vertex Array Object  
	glBindVertexArray(vaoID[0]); // Bind our Vertex Array Object so we can use it

Binding objects
---------------

Steps 3 and 4 above are the 'Binding Objects' part::

	glGenBuffers(1, vboID); // Generate our Vertex Buffer Object  
	glBindBuffer(GL_ARRAY_BUFFER, vboID[0]); // Bind our Vertex Buffer Object  
	glBufferData(GL_ARRAY_BUFFER, 18 * sizeof(GLfloat), vertices, GL_STATIC_DRAW); // Set the size and data of our VBO and set it to STATIC_DRAW

So once steps 1 and 2 have been executed the VAO is bound, which means it is the current VAO we are modifying. All VBOs we create and pass data to (steps 3 and 4) will go into that VAO.

Once we have done step 4, we need to fill our VBO with the vertex data. When creating VBO’s, you can set what type of VBO it is, and in this case we are going for ``GL_STATIC_DRAW``, this tells OpenGL that we do not intend on changing the data in any way, and we just want to be able to render it.

Vertex attributes
-----------------

When we have bound the buffer, we still need to tell OpenGL what it is that we have bound, and we have to tell it which variable in our Vertex Shader it should be assigned to.

What we do is the following::

	loc = glGetAttribLocation(program, "position")
	glEnableVertexAttribArray(loc)
	glVertexAttribPointer(loc, 3, GL_FLOAT, GL_FALSE, 0, 0)

That gets the index of the ``position`` variable in our Vertex Shader.
Then, we enable the ``loc`` index of our currently bound VAO.
Finally, we state that the element in position ``loc`` of our VAO is:

- Of size 3 (e.g. each vertex has 3 elements to it);
- Each element of the vertex is of type ``GL_FLOAT``;
- We do not want OpenGL to normalize the values for us;
- The stride is 0; and
- The offset is 0.

We want to use stride and offset if we want to send multiple different pieces of data in the same buffer.

For example, we would store both position and colour in the same buffer, like so::

	[(-1, 1, 1, 1), (0.235, 0.677, 0.9), (1, -1, -1, 1), (0.113, 0.199, 0.53)]

Imagine every even element (``0`` and ``2``) are position, whereas the others are colour.

We could then pass in the values like so::

	glBindBuffer(GL_ARRAY_BUFFER, self.buffer)  # Bind the buffer that contains both data
	
	loc = glGetAttribLocation(program, "position")
	glEnableVertexAttribArray(loc)
	glVertexAttribPointer(loc, 3, GL_FLOAT, GL_FALSE, 1, 0)  # Give stride of 1 so it skips one element for every element it puts in
	
	loc = glGetAttribLocation(program, "colour")
	glEnableVertexAttribArray(loc)
	glVertexAttribPointer(loc, 3, GL_FLOAT, GL_FALSE, 1, 1)  # As above, but starting at index 1, makes it get the odd elements only

Uniforms
--------

Uniforms are just variables that don't change during the OpenGL rendering.

We can pass them in to our program to define custom state.

For example, we could use an uniform ``vec3 colour`` variable if we wanted to only use that one colour for all our objects that get drawn using the shader.

We can pass uniform values to our shaders like so::

	color_mode_id = glGetUniformLocation(compiled_shader_program, "colormode")
	glUniform1i(color_mode_id, 1)

There are many ``glUniform<xx>`` functions.

The number specifies how large the variable is (only accepts value 1 unless the letter ``v`` is at the end).
If we pass ``1`` then it is just a number, anything else is a vertex of size ``x``.
The letter at the end specifies the type. ``i`` is an integer, ``f`` is a float, ``v`` is a vector.

Vertex and fragment shaders
---------------------------

Vertex
^^^^^^

The inputs to the vertex shader are vertices and their related attributes.

The outputs of the vertex shader are:

- Clip-space vertex positions;
- Texture coordinates;
- Point sizes;
- Colours and fog coordinates; and
- Potentially other custom vertex attributes as well.

At minimum, they must return the **clip-space vertex positions**!

Fragment
^^^^^^^^

These calculate the colours of the individual pixel fragments.

Gets the input from the rasterizer (which fills in the polygons being sent through the graphics pipeline).

Typically used for lighting effects, shadows, bump mapping, and colour toning.

Inputs:

- Pixel fragments and all their attributes.

Outputs:

- Pixel fragment colours.

Other shaders
-------------

Geometry
^^^^^^^^

- Can add and remove vertices from a mesh 
- Can be used to generate geometry procedurally 
- Can add detail to existing meshes 
- Output is then sent to the rasteriser. 

Tessellation
^^^^^^^^^^^^

- Geometry split into “patches”. Tessellation shader inputs and outputs patches.
- Can be used to increase resolution of a geometry by adding patches or splitting a patch into multiple patches.