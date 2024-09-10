GitHub R
==============================

.. _r_package:

Creating an R Package
-----------------------------

This guide is largely excerpted from https://tinyheero.github.io/jekyll/update/2015/07/26/making-your-first-R-package.html

Obtain `devtools <https://cran.r-project.org/web/packages/devtools/index.html>`_ for building packages and roxygen2 to aid in documentation.

.. code-block:: console

   install.packages('devtools')
   install.packages('roxygen2')

In RStudio, navigate to the location where the folder for your package will go, which should be the base of your github directory.

.. code-block:: console

    setwd("C:/Users/j186b025/Documents/GitHub")

Create the framework for the R package using devtools:

.. code-block:: console

    devtools::create('myfirstpackage')

This ends up creating a folder with the same name as your package name with 4 files inside the folder:

DESCRIPTION: This is where all the meta-data about your package goes. Rather than try to explain the contents, I will refer you to Hadley’s detailed explanation on the contents of this file.
myfirstpackage.Rproj: This is a RStudio specific file. As I do not use RStudio, I will not comment on this file as I never use it.
NAMESPACE: In short, this file indicates what needs to be exposed to users for your R package. From my experience, I’ve never edited this file as devtools takes care of the changes as you’ll see below.
R: This is where all your R code goes for your package.
You now have the bare bones of your first R package. First start by filling out the details in the DESCRIPTION file. When that is done, we can start adding some functions!

In RStudio, click ```File > Open Project in New Session...``` 
