---
title: Documenting pipelines
description: Standard way to document cgat-core based pipelines within the OCMS
published: true
date: 2023-09-25T15:35:32.903Z
tags: pipelines, sop, documentation
editor: markdown
dateCreated: 2023-09-25T15:35:32.903Z
---

# Creating documentation

Although it is somewhat redundant, we try to keep code documentation both within pipeline scripts (as reStructuredText) but also rendered in github through the `README.md`.

## Basic workflow

1. Document in the pipeline script as you go using reStructuredText (rst) format. This is done both for general information about the purpose and running of pipelines but also for each task/function contained within the pipeline. If we want to in the future the documentation can be generated using for example [Sphinx](https://www.sphinx-doc.org/en/master/).

2. Copy the relevant aspects of the documentation to a new file named README.rst and convert it to a README.md using pandoc

```
pandoc README.rst -s -o README.md
```
    
This will create the `README.md` that is rendered on the github repo page.

## ReStructuredText (rst)

ReStructuredText is a plaintext markup language that for all intents and purposes serves the same function as markdown. Python code typically uses rst to generate docstrings that explain functionality of code etc. As OCMS pipelines are currently written in the cgat-core framework (python based), reStructuredText is used to document the code.

At the top of the pipeline script you should have the overall documentation for the code, formatted using reStructucturedText. The following sections should be included in this section.

```
"""
============================
Pipeline title goes here
============================

--------
Purpose
--------

Explain the purpose of the pipeline.

-------------
Installation
-------------

How do you install the pipeline i.e. what dependencies does it have and how to install them.

----------------------
Running the pipeline
----------------------

Explain how to run the pipeline. It is often useful to have subheadings here for things like input files, parameterisation and output files. E.g.,

Input files
-----------

Explain the format of input files

Parameterisation
-----------------
Explaing how to set parameters - this will be through a pipeline.yml configuration file. You do not need to go through every parameter but you should reference any additional information people might need in order to successfully run the pipeline.

Output files
-------------
Explain what the outputs are and what they look like in terms of format.

"""
```

After this overview and detailed explanation of the pipeline will come the pipeline code. Each function/task will also have its own docstring (although these will not be displayed on github).


## Function and task documentation

Each task in the pipeline should have a statndard python docstring that explains what the task is for. For example

```
@transform(task1, task2_output)
def task2(infile, oiutfile):
    """
    Explain what the task is doing. 
    Explain what the inputs are.
    Define paramters.
    Explain what the outputs are.
    """
```

This is useful for code documentation and can be used by things like Sphinx to build python documentation. They are not neccessary for the `README.md` in the github repository so while you should ensure that each task and fuction has associated documentation it will not be seen unless someone goes into the code.


## Example documentation

There will be more doctrings and documentation contained within a pipeline script than is neccessary. Therefore to create a `README.md` on github that contains enough information you should copy the top of the pipeline script into a `README.rst` file. This file will contain all of the overview information but not any of the code or the docstrings associated with the code. An example of the Rst documentation for a pipeline can be found for [OCMS_16S](https://github.com/OxfordCMS/OCMS_16S/blob/master/README.rst) and looks like the below.

## Creating a `README.md` from a `README.rst`

You will need to have pandoc loaded to do this. Go into the repository where the `README.rst` is located and type:

```
pandoc README.rst -s -o README.md
```

This will create the `README.md` file that will be visible on the repo's github.
