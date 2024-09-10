R Packages and GitHub
==============================

.. _r_package:

R Package Setup
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

This creates a folder with the same name as your package with four files in it:

DESCRIPTION: Package metadata, see `here <http://r-pkgs.had.co.nz/description.html>`_
myfirstpackage.Rproj: Open this in RStudio to load your entire project for working on. 
NAMESPACE: In an R package, some functions are available to the user, and some are internal functions not exposed to the user. NAMESPACE is a list of exposed functions for the user. Do not edit this by hand. Instead, devtools will manage this file.
R: This is where all your R code goes for your package.

Package Framework
----------------------------

In RStudio, click ``File > Open Project in New Session...`` and navigate to your new ``myfirstpackage`` folder and open ``myfirstpackage.Rproj``. 

Start by creating some .R files to contain your functions. I organize my functions as follows:

* **interface.R**: contains all functions exposed to the user

* **load.R** and **save.R**, or **io.R**: Input/Output functions for importing data or writing data to file

* **process.R**: Functions for manipulating imported data

* **figures.R**: Creating and saving figures

* **util.R**: small utility functions

* project-specific groupings of functions can get their own files as well

Within each ``.R`` file, I prefix internal function names with the filename to aid in locating functions between files while working. 

.. code-block:: console

    LOAD.import_timecourse <- function(filename){
      #code here
    }

Don't prefix user-exposed functions in ``interface.R``, these should have the function names you want users to use while using your package. In addition, these functions need to have a `#' @export` tag so that ``devtools::document()`` and Roxygen can correctly mark them as exportable functions in NAMESPACE and generate help files.

External Dependencies
-------------------------

Naturally, your functions will require other functions from other packages. Do **NOT** import them in your code with library(packagename). That will add it to the user's environment causing unintended behavior. Instead, write your code such that you call external functions with the double-colon syntax. For example, to create a ggplot figure you would write:

.. code-block:: console

    ggplot2::ggplot(data, ggplot::aes(x = time, y = value)) + ggplot::geom_line()

And in your ``DESCRIPTION`` file, add the packages you need as dependencies in a comma-separated list. You may optionally add minimum version requirements.

.. code-block:: console

    Imports:
        ggplot,
        otherPackage (>= 1.2.0)

If you use the ``%>%`` pipe function from ``magrittr``, you will need to import that function in your namespace for it to work properly. Add the following line to the top of one of your ``.R`` files, and ``devtools::document()`` will add the required code to your namespace to support ``%>%`` in your functions.

.. code-block:: console
    
    #' @importFrom magrittr %>%

Documenting Functions
--------------------------

See https://tinyheero.github.io/jekyll/update/2015/07/26/making-your-first-R-package.html

Including Data for Distribution in your Package
-----------------------

Sometimes it is helpful to include sample data sets in your package. Add them following the guide here:
See https://tinyheero.github.io/jekyll/update/2015/07/26/making-your-first-R-package.html

Distribution with GitHub
--------------------------

First, make a GitHup repository of your package. If you are using GitHub Desktop, Select ``File > New``. Fill out the name and description, and choose the path to the folder that contains your package, i.e., ``C:/Users/j186b025/GitHub`` and click ``Create Repository`` Once It's created, Click ``Publish Repository`` to publish it to GitHub. For your own use, you can keep it a private repository, but if you intend to distribute it you will need to mark it as public (you can start with private and convert to public later in the settings). Do **NOT** put any sensitive or experimental data in your github project folder unless you know what you're doing with the .gitignore file, or it may get publicly published to GitHub. Store your data separately from your code.


