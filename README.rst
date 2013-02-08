================
Plone 4 buildout
================

.. contents ::

Introduction
------------

`Buildout <http://www.buildout.org>`_ is a tool which automatically downloads, installs and configures Python software.
Plone developers prefer uses buildout based installation method - it makes it easy to work with source code and developing your own Plone add-ons.

Prerequisitements
-----------------

What you need in order to use developer buildout with Plone 4

* Experience using command line tools

* Experience using a text editor to work with configuration files (``buildout.cfg``)

* GCC compiler suite to build native Python extensions (Zope contains C code for optimized parts)

* Python 2.7

* Python `Distribute <http://pypi.python.org/pypi/distribute>`_ installation tool, provided by your operating system
  or installed by hand

Read below from operating system specific instructions how to install these dependencies.

Features
--------

This buildout provides

* Zope start up scripts (one instance)

* ``zopeskel`` command for creating Plone add-ons (different from system-wide installation)

* `test <http://plone.org/documentation/manual/plone-community-developer-documentation/testing-and-debugging/unit-testing>`_ command for running automatic test suites 

* `i18ndude <http://pypi.python.org/pypi/i18ndude>`_  for managing text string translations in Python source code 

* `mr.developer <http://pypi.python.org/pypi/mr.developer>`_ command for managing source code checkouts and updates with buildout repeatable manner

Creating Plone 4 buildout installation
--------------------------------------

You need to run (please see remarks regarding your operating system below)::

 $ python2.7 bootstrap.py -dc deploy.cfg

This will create ``bin`` folder and ``bin/buildout`` script. If you any time want to change Python interpreter
associated with buildout, or you need to update ``buildout`` script itself to newer version please rerun ``bootsrap.py``.

Now you can run buildout script which will download all Python packages
(.egg files) and create ``parts/`` and ``var/`` folder structure ::

  $ ./bin/buildout -c deploy.cfg

If this succesfully completes you can start buildout in foreground mode (Press *CTRL+C* to terminate)::

  $ ./bin/zeoserver start
  $ ./bin/instance1 start 

Now you can login to your site

  http://localhost:8010

The default user is ``admin`` with password ``admin``. 
After initial start-up admin password is stored in Data.fs databse file and value in ``buildout.cfg`` is ignored.
Please follow `these instructions to change admin password <http://manage.plone.org/documentation/kb/changing-the-admin-password>`_.

Next steps
----------

Creating your first add-on
==========================

Plone 4 buildout comes with ``./bin/zopeskel`` command for creating Plone add-ons.

Create theme ::

    $ cd src
    $ ../bin/zopeskel plone_basic
    $ cd my.theme/src
	
Create Archetypes based content types package::

	$ ./bin/zopeskel archetype vs.registration

More info

* `Bootstrapping Plone add-on development <http://developer.plone.org/getstarted/paste.html>`_ 

Managing source code checkouts with buildout
============================================

`mr.developer buildout extension <http://pypi.python.org/pypi/mr.developer>`_ command which can be used with buildout to manage your source code repositories
*mr.developer* makes source code checkout from multiple repositores a repeatable task.

Operating system specific instructions 
--------------------------------------

Ubuntu/Debian
=============

Tested for Ubuntu 10.10.

Install prerequisitements::

	$ sudo apt-get install python2.7 wget build-essential python2.7-dev python-setuptools

OSX
===

Install `OSX development tools (XCode) <http://developer.apple.com/>`_ from Apple.

Install `Macports <http://www.macports.org/>`_.

Then the following installs dependencies::

	$ sudo port install python27 py27-distribute wget pcre

When you run ``bootstrap.py``use the following command to make sure you are using Python interpreter from Macports::

	$ python2.7 bootstrap.py

Windows
=======

Microsoft Windows systems is problematic because
it does not provide to Microsoft Visual C compiler (commercial) which is
required to build native Python extensions.

Please read

* http://plone.org/documentation/kb/using-buildout-on-windows

