.. _development-environment:

Development environment
=======================

OpenGL does not ship with a windowing API. This means it cannot create windows for the programs to display on. We must use a windowing API to create the windows (and allow for things like fullscreen). In this document I recommend using `GLFW <http://www.glfw.org>`_, but there are a number of others which you can explore:

	- `freeglut <http://freeglut.sourceforge.net>`_
	- `OpenTK <http://www.opentk.com>`_
	- Windows Forms
	- Gaming environments like SDL, pygame, and others

Python
------

Throughout this document we will be looking at Python code. I will be running the examples on a Mac (which only supports OpenGL 4.1), but everything should be platform-independent.

For a Python project, you only need Python installed (`Python 2.7 <https://www.python.org/downloads/>`_ recommended), and an IDE (`PyCharm <https://www.jetbrains.com/pycharm/>`_ recommended). The ``requirements.txt`` (`read more <https://pip.readthedocs.org/en/1.1/requirements.html>`_) file for OpenGL programming in Python is::

	PyOpenGL>=3.0
	PyOpenGL_accelerate
	numpy>=1.5
	glfw==1.0.1

Go
--

<Waiting for PR...>