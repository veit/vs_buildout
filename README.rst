================
Plone 4 buildout
================

.. contents ::

Introduction
------------

`Buildout <http://www.buildout.org>`_ is a tool which automatically downloads,
installs and configures Python software. Plone developers prefer uses buildout
based installation method - it makes it easy to work with source code and
developing your own Plone add-ons.

Prerequisitements
-----------------

What you need in order to use developer buildout with Plone 4:

* Experience using command line tools
* Experience using a text editor to work with configuration files
  (``buildout.cfg``)
* GCC compiler suite to build native Python extensions (Zope contains C code for
  optimized parts)
* Python 2.7

Read below from operating system specific instructions how to install these
dependencies.

Features
--------

This buildout provides

* Zope start up scripts (one instance)
* ``mrbob`` command for creating Plone add-ons (different from system-wide
  installation)
* `test
  <http://docs.plone.org/manage/deploying/testing_tuning/testing_and_debugging/unit_testing.html>`_
  command for running automatic test suites 
* `i18ndude <http://pypi.python.org/pypi/i18ndude>`_  for managing text string
  translations in Python source code 
* `mr.developer <http://pypi.python.org/pypi/mr.developer>`_ command for
  managing source code checkouts and updates with buildout repeatable manner

Creating Plone 4 buildout installation
--------------------------------------

You need to run (please see remarks regarding your operating system below)::

 $ virtualenv --system-site-packages venv
 $ cd venv
 $ ./bin/pip install zc.buildout
 $ cd ../
 $ git clone https://github.com/veit/vs_buildout.git
 $ cd vs_buildout
 $ ../venv/bin/buildout -c devel.cfg

This will download all Python packages (.egg files) and create ``parts/`` and
``var/`` folder structure.

If this succesfully completes you can start innstance in foreground mode (Press
``ctrl+c`` to terminate)::

  $ ./bin/instance fg

Now you can login to your site::

  http://localhost:8010

The default user is ``admin`` with password ``admin``. 
After initial start-up admin password is stored in Data.fs databse file and the
value in ``buildout.cfg`` is ignored.
Please follow `these instructions to change the admin password
<http://plone.org/documentation/kb-old/changing-the-admin-password>`_.

Creating your first add-on
==========================

Plone 4 buildout comes with ``bin/mrbob`` command for creating Plone add-ons.

Create theme ::

    $ cd src
    $ ../bin/mrbob -O my.theme bobtemplates:plone_addon
    ...
    --> What kind of package would you like to create? Choose between 'Basic', 'Dexterity', and 'Theme'. [Basic]: Theme

Create Archetypes based content types package::

    $ ../bin/mrbob -O my.type bobtemplates:plone_addon
    --> What kind of package would you like to create? Choose between 'Basic', 'Dexterity', and 'Theme'. [Basic]: Dexterity

More info

* `Develop Plone Add ons
  <http://docs.plone.org/4/en/develop/addons/index.html>`_ 

Managing source code checkouts with buildout
============================================

`mr.developer buildout extension <http://pypi.python.org/pypi/mr.developer>`_
command which can be used with buildout to manage your source code repositories
*mr.developer* makes source code checkout from multiple repositores a repeatable
task.

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

    $ sudo port install python27 py27-distribute wget

When you run ``bootstrap.py`` use the following command to make sure you are
using Python interpreter from Macports::

    $ python2.7 bootstrap.py -dc devel.cfg

Windows
=======

Microsoft Windows systems is problematic because it does not provide the
Microsoft Visual C compiler (commercial) which is required to build native
Python extensions.

Please read

* http://plone.org/documentation/kb/using-buildout-on-windows

