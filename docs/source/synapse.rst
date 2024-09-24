Synapse Server Usage
================

`Current server loads <http://hbic-synapse.kumc.edu:3838/usage.html>`_

.. _general:

General
------------------

Synapse and the secondary servers, Alpha/Beta/Gamma/Delta, are general use Linux servers running RHEL8 that can be accessed on and off campus and are suitable for viewing and processing imaging data.

The servers are maintained by James Bartolotti jbartolotti2 at kumc dot edu. To report issues, request new software, get R-Drive or P-Drive access, or a new synapse account, fill out this `Redcap survey <https://redcap.kumc.edu/surveys/?s=R7PCHA3PNL>`_

Selecting a Server
--------------------

**hbic-synapse** is the primary research server, accessible over SSH, with 12 CPU & 24 GB RAM. The secondary servers, **hbic-alpha** and **hbic-beta** are also accessible over SSH and are suitable for resource-intensive interactive jobs such as MATLAB. Check the `current server loads <http://hbic-synapse.kumc.edu:3838/usage.html>`_ and consider connecting to **hbic-alpha** or **hbic-beta** if Synapse is congested.

A SLURM scheduler hosted on Synapse allows you to submit batch scripts to the compute-only servers **hbic-gamma** and **hbic-delta**. Direct SSH connections to these servers is not permitted. The scheduler will wait to submit your job until CPU/RAM resources become available, and will reserve those resources for the duration of your job so that it will not get throttled or killed due to congestion.


.. _networkdrive:

Network Drives
--------------

Local storage on synapse is intended for applications and is not suitable for raw or processed imaging data. All raw imaging data and other Restricted-level data (e.g., data containing PHI) must be stored on the P-Drive. Confidential, non-Restricted data may be stored on the R-Drive. For assistance classifying your data, contact the Office of Information Security and review the `Data Classification Procedure Document <https://kumed.sharepoint.com/sites/mykumc/is/best-practices-forms>`_

Use the "KUMC-Map" and "KUMC-Unmap" utilities to mount network drives to Synapse, including P-Drive, R-Drive, S-Drive, G-Drive, and other lab-specific drives. To run, add any number of drive arguments in brackets below (do not include the brackets in your command). Contact James for assistance adding additional network drives.

.. code-block:: console

   sudo KUMC-Map [R SOM P PNFS S G KUL]
   sudo KUMC-Unmap [R SOM P PNFS S G KUL]


* **R**: R-Drive, "//kumc.edu/data/Research/Hoglund"

* **SOM**: R-Drive, "//kumc-data01/Research/SOM RSCH"

* **P**: P-Drive, CIFS protocol.

* **PNFS**: P-Drive, NFS protocol (preferred). This will become the default P-Drive mount protocol in 2024.

* **S**: S-Drive

* **G**: G-Drive

* **KUL**: Mosconi Lab drive at KU-Lawrence

Applications
---------------------

Not all applications are available on the system path by default. Use the "loadapps" utility to add software to your startup script. 

.. code-block:: console

   loadapps

Available applications (load before first use with loadapps):

* ASHS
* MRIcron
* AFNI
* lcmodel
* TORTOISE
* MATLAB
* itk-SNAP
* Mango
* Fiji
* AlizaMS
* Freesurfer
* ImageJ
* SegAdapter
* ANTs
* Mipav
* FSL

Additional applications are always available at the command line, including R, Python, Docker, Singularity, Firefox, and Okular (pdf viewer). See more with ``ls /usr/local/bin``

Python environments are managed with ``conda``. See available conda environments with ``ls /opt/anaconda3/envs`` and activate an environment with, e.g.:

.. code-block:: console

    conda activate py3_afni_tiny

SLURM Job Management
----------------------

SLURM allows you to submit jobs to the compute nodes **hbic-gamma** and **hbic-delta** from Synapse. Your job will be scheduled and as soon as resources become available on one of the compute nodes. While running, your job will have dedicatad CPU/RAM allocated to it, ensuring that your scripts do not get throttled or killed due to resource competition.

Before running jobs with SLURM, ensure that your account has access to the R and P drives on both **hbic-gamma** and **hbic-delta** with the `checkdrives` command. (The SLURM scheduler will submit your job to the next available node, so be sure that your drives are available on both). 

.. code-block:: console

    checkdrives

The following output indicates that the P-Drive is available on both servers, but the R-Drive has not been mounted on either server yet.

.. code-block:: console

    hbic-gamma: R-Drive not mounted
    hbic-delta: R-Drive not mounted
    hbic-gamma: P-Drive OK
    hbic-delta: P-Drive OK

Use ``checkdrives`` with a drive letter argument (R and/or P) to mount the requested drive on both **hbic-gamma** and **hbic-delta**, providing your password when requested.

.. code-block:: console

    checkdrives R

To submit a job, create a script file as below, supplying your information in the #SBATCH paramaters. Your job will wait to be scheduled until the requested CPUs and RAM become available. Your job will run up to the time parameter, at which point it will be terminated. Any code you want to execute goes below the #SBATCH lines. If you need a certain application, load it at the beginning of your script with e.g., ``load afni``.

.. code-block:: bash

    #!/bin/bash
    #SBATCH --job-name=testing_slurm         # Job name
    #SBATCH --mail-type=BEGIN,END,FAIL       # Mail events (NONE, BEGIN, END, FAIL, ALL)
    #SBATCH --mail-user=ADDRESS@kumc.edu     # Where to send mail
    #SBATCH --ntasks=1                       # Number of parallel tasks, usually 1
    #SBATCH --cpus-per-task=4                # Number of CPU cores per task
    #SBATCH --mem=1g                         # Total memory requested on the node
    #SBATCH --time=1-00:00:00                # Time limit days-hrs:min:sec
    #SBATCH --output=test_%j.log             # Standard output and error log

    echo "Slurm test successful" > ~/R-Drive/YOUR_FOLDER/slurm_test.txt

To submit a job, run:

.. code-block:: console

    sbatch myscript.sh

And check the status of the compute nodes and your job with:

.. code-block:: console

    sinfo
