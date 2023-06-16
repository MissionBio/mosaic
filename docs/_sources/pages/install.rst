Installation
=============

Installer (Preferred)
---------------------

The installer for Mosaic can be downloaded from the `Mission Bio Portal <https://portal.missionbio.com/>`_.
This is an interactive installer for Mac and Windows, and a shell script for Linux. It has
all the packages in it and doesn't require an internet connection to install.

Installing using conda
----------------------

Although this method is prone to errors due to updates to dependencies of mosaic causing incompatiblity,
it is possible to install Mosaic through the `missionbio conda channel <https://anaconda.org/missionbio>`_.

1. Install Anaconda
    First install the appropriate version of anaconda for your device from the `Anaconda page <https://www.anaconda.com/products/distribution>`_

2. Ensure that the `libmamba` solver is being used:
    The `libmamba <https://www.anaconda.com/blog/a-faster-conda-for-a-growing-community>`_ solver is
    a new dependency solver that is much faster than the default solver. Install it using the following:

   .. code-block:: bash

      > conda install -n base conda-libmamba-solver
      > conda config --set channel_priority strict
      > conda config --set solver libmamba

3. Install Mosaic
    Following the successful installation of Anaconda, open your console/terminal and run the following commands:

    .. code-block::

        > conda create --name mosaic -c missionbio -c conda-forge missionbio.mosaic

4. Open mosaic environment and jupyter notebook:
    When you want to access your mosaic environment and open a jupyter notebook, always run the following
    commands in your console/terminal. Be sure to keep the console/terminal open and running the entire time
    you are using your notebook, however, you can minimize this window during use. If you are properly in
    your mosaic environment, you will notice the command prompt change from ``base`` to ``mosaic``, please
    ensure this has happened before opening your jupyter notebook, or else the notebook will not function
    properly

    .. code-block::

        > conda activate mosaic
        > jupyter notebook

    Example of prompt changing:

    .. code-block::

        (base) C:\WINDOWS\system32> conda activate mosaic
        (mosaic) C:\WINDOWS\system32> jupyter notebook


    You may get the error “Conda command not found” when trying to go through this for the first time. If so, use the command “source ~/.bashrc”


.. hint::

    If the conda env `mosaic` already exists, remove it using

    .. code-block::

        conda remove --name mosaic --all --yes

Older versions
--------------

Available older versions of mosaic can be found on the `conda channel <https://anaconda.org/missionbio/missionbio.mosaic/files>`_.
These can be installed by passing the required version number.

.. code-block:: bash

    conda create --name mosaic -c missionbio -c plotly -c conda-forge missionbio.mosaic=1.8.1 notebook

Versions tagged with a label besides `main` can be installed by changing the channel name

.. code-block:: bash

    conda create --name mosaic -c missionbio/label/unsupported -c plotly -c conda-forge missionbio.mosaic=1.7.1 notebook
