Installation
=============

Installer (Preferred)
---------------------

The installer for Mosaic can be downloaded from the `Mission Bio Portal <https://portal.missionbio.com/>`_.
This is an interactive installer for Mac and Windows, and a shell script for Linux. With the default settings
the installer will create a directory called ``mosaic`` and install the latest version of Mosaic in it. For Mac
and Linux the installer will also make this version of Mosaic available from the command line by default. For
Windows, ``conda`` is available from the command line if the option to **add to PATH** is selected.

After the installation completes, open the terminal and run:

.. code-block:: console

   $ conda env list

This will output a list of all the available conda environments. If the installation was successful, you
should see a directory called ``mosaic``. The ``*`` next to the environment name indicates the currently
active environment. There might be other directories like ``anaconda`` or ``miniconda`` depending on
previous installations of those packages. The output should look something like this with ``name``
replaced with your username:

.. code-block:: console

                    /Users/name/miniconda3
   base          *  /Users/name/mosaic

**Only if** ``mosaic`` is not the active environment (The ``*`` is next to ``/Users/name/miniconda3`` or
some other environment), activate it using:

.. code-block:: console

   $ conda activate /Users/name/mosaic/

Installing using conda
----------------------

Although this method is prone to errors due to updates to dependencies of mosaic causing incompatiblity,
it is possible to install Mosaic through the `missionbio conda channel <https://anaconda.org/missionbio>`_.

1. Install Anaconda
    First install the appropriate version of anaconda for your device from the `Anaconda page <https://www.anaconda.com/products/distribution>`_

2. Ensure that the `libmamba` solver is being used:
    The `libmamba <https://www.anaconda.com/blog/a-faster-conda-for-a-growing-community>`_ solver is
    a new dependency solver that is much faster than the default solver. Install it using the following:

   .. code-block:: console

      $ conda install -n base conda-libmamba-solver
      $ conda config --set channel_priority strict
      $ conda config --set solver libmamba

3. Install Mosaic
    Following the successful installation of Anaconda, open your console/terminal and run the following commands:

    .. code-block:: console

       $ conda create --name mosaic -c missionbio -c conda-forge missionbio.mosaic

4. Open mosaic environment and jupyter notebook:
    When you want to access your mosaic environment and open a jupyter notebook, always run the following
    commands in your console/terminal. Be sure to keep the console/terminal open and running the entire time
    you are using your notebook, however, you can minimize this window during use. If you are properly in
    your mosaic environment, you will notice the command prompt change from ``base`` to ``mosaic``, please
    ensure this has happened before opening your jupyter notebook, or else the notebook will not function
    properly

    .. code-block:: console

       $ conda activate mosaic
       $ jupyter notebook

    Example of prompt changing:

    .. code-block:: console

       (base) C:\WINDOWS\system32> conda activate mosaic
       (mosaic) C:\WINDOWS\system32> jupyter notebook


    You may get the error “Conda command not found” when trying to go through this for the first time. If so, use the command “source ~/.bashrc”


.. hint::

    If the conda env `mosaic` already exists, remove it using

    .. code-block:: console

       $ conda remove --name mosaic --all --yes

Older versions
--------------

Available older versions of mosaic can be found on the `conda channel <https://anaconda.org/missionbio/missionbio.mosaic/files>`_.
These can be installed by passing the required version number.

.. code-block:: console

   $ conda create --name mosaic -c missionbio -c plotly -c conda-forge missionbio.mosaic=1.8.1 notebook

Versions tagged with a label besides `main` can be installed by changing the channel name

.. code-block:: console

   $ conda create --name mosaic -c missionbio/label/unsupported -c plotly -c conda-forge missionbio.mosaic=1.7.1 notebook

Troubleshooting
---------------

Error in the installer
~~~~~~~~~~~~~~~~~~~~~~

Solutions to many installation failures are available in the `Anaconda troubleshooting <https://docs.anaconda.com/free/anaconda/reference/troubleshooting/>`_
guide. The same solutions can be applied to the Mosaic installater.

Unable to update using the installer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The installer does not automatically delete the previous version of Mosaic. If the directory in which
the new version of mosaic is being installed is not empty, the installer will not be able to install
the new version. Delete the directory or change the installation directory and try again. The default
installation directory is called ``mosaic`` in the home directory of the user.

Failure to save images using ``fig.write_image`` on Windows 11
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Certain version of the ``python-kaliedo`` package might not be compatible with specific versions of Windows 11.
Installing a different version of kaleido might solve the issue. To do so, activate the Mosaic environment,
then install the ``python-kaleido`` package:

.. code-block:: console

   $ conda install -c conda-forge python-kaleido=0.1.0

Then relaunch the jupyter server and run the notebook again.
