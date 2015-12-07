.. _texture-and-coloring:

Texture and coloring
====================

Antialiasing
------------

Simply send the ``GLFW_SAMPLES`` window hint when creating the window::

	glfw.init()
	
	glfw.window_hint(glfw.SAMPLES, 4)

Then, enable ``GL_MULTISAMPLING``::

	gl.glEnable(GL_MULTISAMPLING)
