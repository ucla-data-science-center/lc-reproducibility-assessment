---
title: Code Execution
teaching: 0
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Understand the importance of the code execution tasks to curating for reproducibility
- Recall some of the common issues that prevent code from fully executing
- Perform the code execution process as part of a reproduciblity assessment

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What does it mean to execute code in the context of a research compendium?
- What can be done prior to publication to ensure that code will run error-free?
- What are some of the common errors that cause non-executable code?

::::::::::::::::::::::::::::::::::::::::::::::::::

After inspecting the code to be sure it includes all of the elements required to achieve reproducibility, the next step in the curating for reproducibility workflow is to run the code to confirm that it executes without errors and produces the outputs that match the results reported in the manuscript. This episode explains the process of running the code and describes some of the most common code errors encountered during reproducibility assessments.

## Code Execution Overview

As the first reusers of the research compendium, curators can identify and address issues in the compendium that compromise standards for reproducibility *before* results are published in a report or manuscript.  Not only does the curator inspect compendium files, but also, they verify that the files function as they should by using them to retrace the analytical workflow and reproduce reported results. This gives researchers assurances that research compendia they make available to the public meet high quality standards for reproducibility.

Executing the code provided in the research compendium is a critical step in assessing reproducibility, which requires that the research compendium be ***independently understandable*** and ***reusable***.  In practical terms, this means that anyone should be able to download the compendium and run the code to analyze the data and produce expected outputs--without having to modify the code or input data, *and* without assistance from the researcher(s) who originally wrote the code and performed the analysis.

Executing code as part of the code review process is not a common activity for many library and information professionals. However, adding this practice to curation and repository ingest workflows is imperative if reproducibility is the goal.

## Running the Code

Prior to running the code, the computing environment will need to be set up according to the information provided in the research compendium.  The initial code inspection, along with the data review, should give a good sense of the technical specifications for running the code.

When setting up the computing environment for running the code, consider the following:

**Does the computing environment to be used to run the code meet the same or comparable technical requirements as described in the code header metadata (or in the README file)?**  
Differences in operating systems and software versions can yield discrepancies in outputs. Thus, the computing environment used to run the code for reproducibility assessment should match the provided specifications as closely as possible.

**Does the code automatically install required packages or indicate in the header metadata how packages will need to be installed manually?**  
When running code to assess reproducibility, use the base (i.e., fresh) installation of the statistical software program *without* packages and libraries pre-installed.  The base installation allows for detection of packages and libraries needed by the code to run correctly.

**Can the code be run in a single sitting, or will the computation require more than one session?**  
Take note of the estimated run time required to execute the code.  Complex or resource-heavy computations or analyses that use big data can take a significant time to run from beginning to end.

> ## Spotlight: Capturing Information About the Computing Environment
> 
> There are specific commands that can help provide information about the computing environment or session while also identifying the packages necessary to run the code properly.  While this information should be included in the code header metadata and/or elsewhere in research compendium documentation, curators can use these code commands to obtain this information if it is missing from the compendium.
> 
> ```
> # Print version information about R, the OS, and packages
> ```

sessionInfo()

:::::::::::::::::::::::::::::::::::::::::  callout

## Print version information about the "pkg" package

packageVersion("pkg")

```
{: .source}
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Exercise: Let's Run Some Code!

Open the sample code file and run the code. Did it run successfully?

:::::::::::::::  solution

## Solution

If the code ran correctly using the specified software version, you should see this:

[IMAGE]

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Spotlight: What About Containers?

Rather than enabling scripts to run on different machines, constraining the execution environment to a specific operating system and specific dependencies may make it easier to ensure re-execution.

A common approach to making it easier to rerun code is to do the computation on a cloud-based service or platform. Examples of this approach include [WholeTale](https://wholetale.org/), [Code Ocean](https://codeocean.com/), and [MyBinder](https://mybinder.org/). Many of these are services are built on top of JupyterHub or RStudio, which encapsulate the compute environment in a container.

For desktop based workflows, the computation environment can be fixed in place using a number of solutions such as using a virtual machine or containerisation. This can be done by carefully constructing images or build scripts to use [Vagrant](https://www.vagrantup.com/), [Docker](https://www.docker.com/) or [Singularity](https://sylabs.io/), usually starting with an image or container that includes all or most of the software required.

The image or container might be a suitable target for archiving (being mindful of licensing restrictions), or the scripts and/or config files that describe how to build the image or container, fetch the appropriate code and data, and then combine them is a potential approach for longer-term preservation of research compendia.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Common Code Issues

There are many reasons that code may not run properly. Oftentimes, it is not the fault of the researcher who originally wrote the code.  As mentioned previously, differences in operating systems may affect the mechanics of the computation or cause discrepancies in the computational outputs. Software is often updated with bug fixes, new features, and other changes in ways that do not allow for backwards compatibility.

Other reasons that code may not execute fully (or not at all) may have something to do with the way the code was written. Below are some of the issues that are caused by faulty code.

### Syntax errors

A simple typo in lines of code can cause syntax errors that cause code execution to fail.  Running the code from beginning to end will catch these easy-to-fix errors.

### Missing comments

Code that is written with reproducibility in mind will include non-executable comments that map code blocks to the tables, figures, and in-line results presented in the publication.  The absence of such signposts, which will not necessarily cause code execution errors, still make reproducibility assessment cumbersome.

### Use of absolute file paths

Absolute file paths assume that re-users have on their computer workstation a file directory structure identical to that of the original researcher.  When it is not the case that the file directory is identical, running the code will result in an error indicating that the file cannot be found.  Using relative paths makes the research compendium portable by calling files relative to its location in the current working directory.

```source
# Read in the data file using an absolute file path
read.csv ("C:/Users/Documents/PopStudy1/Data/AnalysisData/pop1_analysis_data.csv")

#  Read in the data file using an absolute relative file path.
read.csv ("./PopStudy1/Data/AnalysisData/pop1_analysis_data.csv")
```

### Missing package installation scripts

Scripts to install packages are required to successfully execute the code (i.e., prerequisites).  Without package installation scripts, the code will fail to execute until the packages are installed and loaded.

```source
* Create Prerequisite folder and put cluster2.ado in this folder
sysdir set PLUS ..\Prerequisites
ssc install outreg2
ssc install wyoung
```

### Missing seed

Any computation that generates random numbers (e.g., Monte Carlo simulations) requires a set seed to initialize the algorithm that generates the random numbers.  Without that specific seed, the code will generate different random numbers, which will produce different outputs each time the code is run.

```source
# Below, no seed is set so that every time the code is run, the output will be different.
# set year list 
yearsets <- split(sample(years, length(years)), cut(seq(1,length(years)), breaks-ks, labels=FALSE))

# Below, the seed is set so that every time the code is run, the output will be the same.
# set year list
set.seed(123) # set seed for random number generation
yearsets <- split(sample(years, length(years)), cut(seq(1,length(years)), breaks-ks, labels=FALSE))
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Exercise: Troubleshooting Problem Code

Run the code file that contains faulty code.

Answer the following questions:

- What issues did you encounter when executing the code?
- How might the issues be resolved so that the code runs successfully and produces the anticipated outputs?

:::::::::::::::  solution

## Solution

solution

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Spotlight: Coding Best Practices

Even code that executes properly can use some improvements to make it more readable and more efficient or elegant. This in turn can enhance reproducibility by making code that may appear to be "messy" to some users easier to understand and follow the sequence of analytical operations.

One way that code can be made more readable is to **address how the code represents the sequence of operations** so that the presentation of code blocks makes logical sense.  Beyond inserting non-executable comments throughout the code to indicate what lines of code are meant to do or what the code is meant to produce, presenting code blocks in the same order in which corresponding results appear in the manuscript (if feasible to do so), makes it less cumbersome to assess reproducibility.

Another opportunity to improve code is to **address inefficiencies** in the code.  A script may include commands that achieve a specific outcome, but do so inefficiently. For example, a script that includes repeated statements when other expressions are more appropriate like in the example below:

```
* Inefficient code
SFA = SSMR1_N + SSPM1_N + SSST1N + SSAR1_N + SSDA1_N + SSLG1_N;
if SSMR1_N = . then SFA = .;
if SSPM1_N = . then SFA = .;
if SSST1_N = . then SFA = .;
if SSAR1_N = . then SFA = .;
if SSDA1_N = . then SFA = .;
if SSLG1_N = . then SFA = .;

* Efficient code that achieves same output as inefficient code above
SFA = sum(SSMR1_N, SSPM1_N, SSST1N, SSAR1_N, SSDA1_N, SSLG1_N) 
SFA = sum(SSMR1_N, SSPM1_N, SSST1N, SSAR1_N, SSDA1_N, SSLG1_N na.rm = TRUE)
```

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- Executing code tests the reusability of the research compendium, which is a fundamental criterion of reproducibility.
- Prior to running the code, the computing enviroment will need to meet the same or comparable techinical requirements as described in compendium documentation.
- Simple errors that prevent code from fully executing can be easily addressed.

::::::::::::::::::::::::::::::::::::::::::::::::::


