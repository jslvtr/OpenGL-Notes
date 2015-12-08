.. _aliasing:

Aliasing and Anti-aliasing
==========================

Simply send the ``GLFW_SAMPLES`` window hint when creating the window::

	glfw.init()

	glfw.window_hint(glfw.SAMPLES, 4)

Then, enable ``GL_MULTISAMPLING``::

	glEnable(GL_MULTISAMPLING)
