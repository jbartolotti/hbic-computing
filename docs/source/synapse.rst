Synapse Server Usage
================

.. _general:

General
------------------
Synapse is a general use Linux server running RHEL8 that can be accessed on and off campus and is suitable for viewing and processing imaging data.

The server is maintained by James Bartolotti jbartolotti2 at kumc dot edu. To report issues, request new software, get R-Drive or P-Drive access, or a new synapse account, fill out this `Redcap survey <https://redcap.kumc.edu/surveys/?s=R7PCHA3PNL>`_

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

Not all applications are available on the system path by default. Use the "load" utility to add software for either one-time use or to add it to your ~/.bash_profile startup script. Run "load" with no arguments for a list of available software.

.. code-block:: console

   load afni

   load --save afni

* `AlizaMS <https://github.com/AlizaMedicalImaging/AlizaMS>`_: Dicom Viewer 

  * hbic-synapse: alizams

  * hbic-synapse2: /usr/local/bin/alizams-1.4.2_linux/bin/alizams

* `ANTs <https://github.com/ANTsX/ANTs>`_: Advanced Normalization Tools for MR images

  * hbic-synapse: /opt/ANTS/bin/ANTS

* `Freesurfer <https://surfer.nmr.mgh.harvard.edu/fswiki>`_: An open source neuroimaging toolkit for processing, analyzing, and visualizing human brain MR images

  * hbic-synapse: 
    
    | export FREESURFER_HOME='/usr/local/freesurfer/7.4.1-1'

    | export SUBJECTS_DIR=$FREESURFER_HOME/subjects

    | source $FREESURFER_HOME/SetUpFreeSurfer.sh

    | freesurfer

  * hbic-synapse2: 

    | export FREESURFER_HOME='/usr/local/freesurfer/7.2.0-1'

    | export SUBJECTS_DIR=$FREESURFER_HOME/subjects

    | source $FREESURFER_HOME/SetUpFreeSurfer.sh

    | freesurfer

* `FSL <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSL>`_: A library of analysis tools for FMRI, MRI and diffusion brain imaging data

  * hbic-synapse:

    | FSLDIR=/opt/fsl

    | . ${FSLDIR}/etc/fslconf/fsl.sh

    | PATH=${FSLDIR}/bin:${PATH}

    | export FSLDIR PATH

    | fsl

  * hbic-synapse2:

    | load fsl

    | fsl

* `ImageJ <https://imagej.net/ij/index.html>`_: Image processing and analysis

  * hbic-synapse: /opt/ImageJ/ImageJ

Utilities
---------------------

* Docker & Singularity

* Firefox

* okular (pdf viewer)

