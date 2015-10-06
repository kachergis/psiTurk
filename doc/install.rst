Getting **psiTurk** Installed on Your Computer
===============================================

**psiTurk** can be installed on any modern computer which supports
Python (<= 2.7). However, currently **psiTurk** is *not* supported on
Windows (`see below <#windows>`__). It works well on most unix variants
including Mac OS X, BSD, and Linux. Installation is *usually* not
difficult.

When **psiTurk** is successfully installed, you will simply have a new
command line tool available called ``psiturk``. The ``psiturk`` command
provides a number of functions to you including launching the server
and interacting with the Mechanical Turk and Amazon Web Services (AWS)
systems.

Installation requirements
-------------------------

Installation of **psiTurk** requires:

1. **A python installation (<= v2.7).** We recommend the `Enthough
   python distribution <https://www.enthought.com/products/epd/free/>`__
   on Mac OS X.
2. **The ``pip`` package manager.** Directions on installing this are
   given below.
3. **Access to a command line tool.** (e.g., Terminal.app on Mac OS X)
4. **A web browser.** A WebKit compatible browser such as FireFox,
   Safari, or Chrome is recommended.

An additional requirement for actually using **psiTurk** to run experiments
is a Internet connected computer capable of receiving incoming requests.

Installation steps
------------------

To install the package there are two options currently. First, the
current stable release of **psiTurk** is hosted on the python package
index `pypi <https://pypi.python.org/pypi>`__. As a result, it can
easily be installed as a standard python package using the python
package manager tool ``pip``. Alternatively, you can install directly
from the development or master (i.e., stable) branch on
`github <https://github.com/NYUCCL/psiTurk>`__. The following
instructions describe the general process. In addition, system specific
notes are provided below.

Install stable version via pypi
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The easiest way to install **psiTurk** is via ``pip``. If you don't
already have ``pip``, you can install it by typing the following in a
terminal:

::

    cd /tmp  # Just to put us in a directory that will be cleaned up periodically
    curl -O https://raw.github.com/pypa/pip/master/contrib/get-pip.py
    python get-pip.py  # If you get a permissions error, try typing sudo python get-pip.py

Once ``pip`` is installed, type into a terminal:

::

    pip install psiturk

If this doesn't work, try

::

    sudo pip install psiturk

If the install was successful you will have a new command ``psiturk``
available on your command line. You can check the location of this
command by typing

::

    which psiturk

Install directly from github
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can also install the latest version directly from github using
``pip``. To install the latest stable branch follow the instructions
above to install ``pip`` and:

::

    sudo pip install git+git://github.com/NYUCCL/psiTurk.git@master

or

::

    sudo pip install git+git://github.com/NYUCCL/psiTurk.git@dev

for the bleeding-edge development version. If the install was successful
you will have a new command ``psiturk`` available on your command line.
You can check the location of this command by typing

::

    which psiturk

Updating from a previous version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To avoid compatibility issues, if you upgrade from a previous version it
can be useful to first uninstall then reinstall **psiTurk** using the
following sequence of commands:

::

    $ pip uninstall psiturk
    $ git clone git@github.com:NYUCCL/psiTurk.git 
    $ cd psiTurk
    $ sudo python setup.py install


To use the development tree, the second command should be
``git clone -b dev git@github.com:NYUCCL/psiTurk.git``.

System-specific notes
---------------------

Mac OS X
~~~~~~~~

Apple users will need to install a C compiler via XCode; to do so,
install XCode from the App store. Once you have downloaded it, install
the command line tools from the preferences menu as instructed
`here <http://stackoverflow.com/a/9353468/62179>`__. For earlier
versions of Mac OS X (e.g., Snow Leopard) you may need to install XCode
using the installation disc that came with your computer. The command
line tools are an option during the installation process for these
systems.

Linux
~~~~~

**psiTurk** is relatively painless to install on most Linux systems
since all four of the requirements listed above come installed by
default in most distributions. If you have specific issues please help
us update the documentation!

Windows
~~~~~~~

**psiTurk** is currently not supported on Windows. This is due to a
technical limitation in the ability to run server processes on Windows.
We currently recommend that Windows users try a cloud-based install such
as `openshift <https://www.openshift.com>`__.

Cloud-based install (experimental)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If your local computer does not support **psiTurk** is it still possible
to use the package by using a free hosting solution such as
`openshift <https://www.openshift.com/>`__. Begin by creating an account
at http://openshift.redhat.com/ and download the command line tools at
https://www.openshift.com/developers/rhc-client-tools-install

Create a python-2.7 application and add a PostgreSQL cartridge to the
app

::

    rhc app create psiturk python-2.7 postgresql-8.4 --from-code git://github.com/jbmartin/psiturk-on-openshift.git

or you can do this to watch the build

::

    rhc app create -a psiturk -t python-2.7
    rhc cartridge add -a psiturk20 postgresql-8.4

Add this upstream psiturk repo

::

    cd psiturk
    git remote add upstream -m master https://github.com/jbmartin/psiturk-on-openshift.git
    git pull -s recursive -X theirs upstream master

Then push the repo upstream

::

    git push

That's it, you can now checkout your application at

::

    http://psiturk-$YOURNAMESPACE.rhcloud.com

To access the your openshift hosted database run

::

    rhc port forward -a psiturk

Connect to the database using your favorite SQL app, the PostgreSQL
Local specs, and your credentials.
