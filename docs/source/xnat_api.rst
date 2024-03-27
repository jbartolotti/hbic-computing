XNAT API
==============================

.. _xnat_api:

`XNAT has an API <https://wiki.xnat.org/xnat-api/>`_ for command line querying and interacting with data contained in XNAT.

There are several tools built on top of the API in different programming languages, including Rxnat, pyxnat, and xnatpy.

Rxnat
-----------------------------

`Rxnat <https://neuroconductor.org/tutorials/rxnat>`_ is an R package to facilitate connecting to, querying, and downloading from XNAT.  

It is installed for all users on Synapse. Elsewhere, you can install Rxnat from neuroconductor with:

.. code-block:: console

   library(neurocInstall)
   source("http://neuroconductor.org/neurocLite.R")
   neuro_install("Rxnat", release = "stable")

Alternatively, you can install it from GitHub with:

.. code-block:: console

   # install.packages("remotes") # Uncomment this line to install the 'remotes' package if you get an error on the following line
   remotes::install_github("neuroconductor/Rxnat")

Rxnat Usage
-------------------------

First, connect to and authenticate with xnat. **DO NOT** save your password in your scripts directly. Instead, request the username and password interactively at runtime. The `getPass` library is already installed on Synapse. On a local computer, first install it with `install.packages('getPass')`

.. code-block:: console

   hbic <- xnat_connect('https://xnat.kumc.edu', username = readline('XNAT Username: '), password = getPass::getPass('XNAT Password: '))

There are four levels of data structure that you can access with Rxnat:

- **Project**: A single research study containing multiple subjects. 
- **Subject**: A grouping for an individual, they may have multiple datasets associated with them.
- **Experiment**: A single dataset assigned to an individual subject. Each scanning session is sent to XNAT as an individual experiment.
- **Resource**: A single file in an experiment. Each DICOM image is a separate resource.

Each level can be queried from Rxnat. The functions ``hbic$projects()``, ``hbic$subjects()``, and ``hbic$experiments()`` (replace hbic with the name of the variable you saved the output of xnat_connect() to). Return tables with information on all projects, subjects, or experiments in XNAT that you have access to. ``hbic$get_xnat_experiment_resources(EXPERIMENT_ID)`` returns a table with all resource files associated with the given experiment. ``EXPERIMENT_ID`` refers to an ID from the ``hbic$experiments()`` table, and is also called the "Accession #" in the XNAT web interface.

.. image:: media/xnat_rxnat.png
     :width: 800


To obtain the resource files associated with a particular scan, you will need to provide either the URI (Universal Resource Identifier) for each file, or the XNAT ID associated with a single Experiment. The XNAT ID is labeled "Accession #" on the Experiment details page for the scan.



