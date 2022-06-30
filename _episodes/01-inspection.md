---
title: "Code Inspection"
teaching: 0
exercises: 0
questions:
- "Why inspect the code?"
- "What is the purpose of code comments?"
- "What is code header metadata, and why is it important?"
- "What is a Main File, and why is it important?"
objectives:
- "To understand the importance of code comments for reproducibility"
- "To understand the importance of code header metadata for reproducibility"
- "To understand what a Main File is and how it contributes to reproducibility"
keypoints:
- "A Main File is an essential piece of code supplementing a README file and often the starting point in a fully automated push-button replication.  A must-have in reproducibility packages that have more than one program file."
- "Code header metadata signals to re-users the code authors’ transparency and willingness to be contacted, identifies the appropriate computing environment to run the analysis, and permission to use the code(s)."
---
Assessing the reproducibility of scientific claims involves an exhaustive list of curation actions, which are outlined in the Data Quality Review (DQR) framework introduced in [Lesson 2: Curating for Reproducibility Workflows]() of the Curating for Reproducibility Curriculum. DQR organizes these curation actions into four components--file review, documentation review, data review, and code review--each of which promote reproducibility by ensuring the completeness, accuracy, understandability, accessibility, and usability of the research compendium.

Code review, in particular, puts reproducibility to the test by verifying whether or not repeating the analytical steps used by the original researcher produces the same results reported in the published study. This assessment of reproducibility begins with a thorough code inspection.

## Code Inspection Overview

Ideally, researchers, who know their work best and have direct access to all the necessary details of their analytical workflow, would inspect their code before they share it to be sure that all of the scripts needed to load software packages, import and transform data, and produce outputs are included in code files. They would review their code to be sure that computing environment requirements and the expected runtime are specified in code header metadata and that non-executable comments are included throughout the code to serve as signposts for the analytical workflow by indicating the purpose of commands. They would also confirm that their files render properly, and re-run their code (preferably on a machine other than the one used to perform the original analysis) to be sure that the code compiles properly and executes the analysis from beginning to end without errors. 

Unfortunately, it is not always the case that researchers review their code for understandability and executability prior to packaging it into the research compendium and sharing it.  Thus, the first step of any reproducibility assessment is to inspect the code and confirm that it includes the following: 

- Sufficient information to enable users to re-create the computing environment originally used to run the analysis and produce the reported results 
- Details about the analytical workflow that allows others to understand and re-trace the computational steps to produce expected outputs
- Scripts for installing necessary software tools and importing data that take into account independent reuse of the code by researchers other than those who initially wrote the code and ran the analysis 

## Code Elements

The simple act of opening a code file is an essential part of code review.  Doing so confirms that the file has not been corrupted and allows for an inspection of the code to determine whether or not it includes all of the elements needed to retrace the analytical steps to generate expected outputs. 

Note that while code files generally require specific statistical software to render properly, opening a code file using a text editor may be sufficient enough for an initial inspection.  The image below shows an example of a typical code file with the essential elements highlighted:

![Code elements]({{ page.root }}/fig/01-code-elements.jpg "Code elements")

## The Analytical Workflow

By its very nature, the analytical workflow of computational research is captured in the code that contains the commands to install software package dependencies, import and transform data, and execute scripts to analyze data and produce results.  

It is also the nature of research that analytical workflows are rarely linear, which is often reflected in code that produces outputs in a different order than the order in which they are presented as research results in the manuscript. This makes it necessary for the code to provide signposts to allow others to retrace the analytical steps.  These signposts should appear in the code as non-executable comments found in code header metadata and throughout the code.  

### Code Header Metadata
When inspecting the code, it should be evident the technical requirements for running the code successfully.  This information is presented as code header metadata, which  is a block of non-executable text positioned at the top of the code before any command scripts.

![Code header metadata example]({{ page.root }}/fig/01-code-header.jpg "Code header metadata example")

Code header metadata should provide enough information to allow others to recreate the computing environment used to run the analysis. It should also specify acceptable uses of the code with a license, and provide contact information for the creator(s) of the code in the event that challenges arise when attempting to reproduce the analysis. 

> ## Checklist: Code Header Metadata
> 
> This checklist outlines the specific information that should be included in code header metadata for every code file.  A code inspection should confirm the presence of each item in the checklist.
>
> -  Formal citation for the article that presents the results produced from the code  
> - Author contact information including email, affiliation, and ORCID  
> - Code license that specifies allowable uses and conditions for use of the code  
> - Computing environment specifications:  
>   - Operating system and version  
>   - Number of CPUs/cores  
>   - Size of memory  
>   - Statistical software package and version  
>   - Packages, libraries, and other software dependencies and their versions
> - File encoding  
> - Date that the code was last updated  
> - Date that the code was last run successfully  
> - Estimated time to run the code from beginning to end  
{: .checklist}

> ## Exercise: Code Header Metadata Inspection
>
> Review the sample code and identify each piece of information outlined in the Code Header Metadata Checklist.
>
> > ## Solution
> >
> > 
> >
>
> {: .solution}
{: .challenge}

### Non-executable Comments
The code header metadata is an example of non-executable comments that also appear elsewhere in the code.  Non-executable code comments are lines of human-readable text that can be placed throughout the code without interfering with command scripts that perform analysis workflow actions.  

The syntax for non-executable comments often uses a specified symbol or set of symbols (`*`, `//`, `/**`, or  `#` depending on the programming language placed before the comment text, which signals to the software program that the text should be ignored. 

To add a comment to code written in R, `#` is placed before the comment statement:

~~~
# my comment
~~~
{: .source}

Non-executable comments are like a “note to self” that tells researchers what the code is doing and why.  These annotations remind the researcher who originally wrote the code of the analytical workflow they used to generate their research results, while also making this information clear to other researchers. Code comments that support reproducibility often include explanations of what lines or blocks of code are meant to do or what outputs the code should produce.

![Examples of non-executable code comments]({{ page.root }}/fig/01-code-comments.jpg "Examples of non-executable code comments")

> ## Spotlight: Sometimes Less is More
>
> During the research process, it is not uncommon for blocks of code used to process and analyze data to gradually grow in size as researchers rework or broaden their approach.  Oftentimes, these code blocks end up including  lines of code that are no longer required to run the analysis and/or producing unnecessary outputs.  
Some researchers may decide that the unneeded code has some potential to be useful, whether to document previously used analytical steps or to be used in subsequent analyses.  In these cases, these lines of code are not deleted, but instead commented out so that they are no longer executable.  
>
> On the other hand, if the code has no role in the analysis and no potential value, it is preferable that this extraneous code be deleted entirely to reduce the amount of lines of code that need to be inspected.
{: .callout}

### The Main File

In some cases, the analysis workflow is complex enough to require more than one code file to produce results.  For research compendia that contain more than one code file, it is highly recommended to use file names that indicate the order in which they must be run and/or provide this information in the README file (see Episode 3: Documentation Review in [Lesson 2: Curating for Reproducibility Workflows]() in the Curating for Reproducibility curriculum for more on the README file).

Use of a **main file**, while not a strict requirement, can do even more to enhance reproducibility.  A main file, when executed, runs all of the other code files in the research compendium in the proper sequence to generate all of the tables, figures, and in-text results presented in the manuscript. It also provides an overview of how the code files are interconnected, which makes it easier to understand and re-trace the analytical workflow.  This makes the main file the starting point for fully automated push-button reproducibility, which is what curating for reproducibility hopes to achieve.

![Main file code example]({{ page.root }}/fig/01-main-file.jpg "Main file code example")

> ## Spotlight: Our Language Choices
>
> Explanation for use of the term “main” rather than “master.”
>
{: .callout}

## Software Dependencies

In some cases, researchers have found that statistical software programs lack functions for performing certain analytical operations. Adept researchers have written custom code themselves and organized it into a reusable package for sharing. This allows other researchers using the same analytical approaches to access and install the package into their own computational environments.

If a study requires the use of certain packages to run the analysis, the research compendium should document this software dependency.  In addition, the code should not assume that users already have the packages installed and loaded.  Rather, the code should include installation scripts for required packages.

When inspecting the code, look for commands that install and load packages into the program environment as in the example below:

~~~
# Install the “analysis” package from CRAN
install.packages(“analysis”)

# Load the “analysis” package into the R library
library(“analysis”)
~~~
{: .source}

##  Data Import

A key function of the code is to point the software program to the data to be used in the analysis, whether that data are included in the research compendium, or are accessed from an external source.  The code inspection examines the commands for reading the data files(s) to determine if the code clearly indicates which data files are used in the analysis and where they are located.  The inspection also checks to see whether the commands are written in a way that enables others to re-run the code without the need to make modifications to make it work correctly. 

### File paths

A file path is used to specify the location of a file within a directory structure.  Take a look at where the `analysisdata.csv` file is located within the directory structure below:
![Data file within a directory structure]({{ page.root }}/fig/01-data-location.jpg "Data file within a directory structure")
File paths are represented as a slash-separated list of the folder names followed by the file name, and can be written as either an absolute file path or relative file path.

**Absolute file paths**  
`C:/Users/Documents/Compendium/Data/analysisdata.RData` is an absolute file path that indicates the location of the `analysisdata.csv` file in relation to a specific root folder and all of the subfolders along the way.

![Absolute file path]({{ page.root }}/fig/01-absolute-path.jpg "Absolute file path")

If the name or location of any one folder along the directory structure changes, the path will be broken, and the code will fail to read the data file. Moreover, using an absolute file path assumes that other users will have the same exact directory structure, which is not likely to be the case.

**Relative file paths**  
`./Compendium/Data/analysisdata.csv` indicates the location of the `analysisdata.csv` file relative to the current directory of the computing environment being used at the moment to run the code.  This relative file path depends on folder names and locations of only part of the directory structure.

![Relative file path]({{ page.root }}/fig/01-relative-path.jpg "Relative file path")

The recommended practice is to use relative file paths instead of absolute file paths because they are  constructed in a way that facilitates reproducibility.  Relative file paths anticipate re-use of the code by other researchers who will certainly use computing environments with varying directory structures.

> ## Exercise: File Paths
>
> To ensure that the analysis code executes successfully in any computing environment, relative file paths should be used to import data.
>
> The data import script below uses an absolute file path. To support reproducibility, convert the absolute file path into a relative file path.
>
> ~~~
> data <- data.csv("H:\Projects\CountryStudy\Data\AnalysisData\country_analysis_data.RData")
> ~~~
> {: .source}
>
> > ## Solution
> >
> > ~~~
> > data <- data.csv("./AnalysisData/country_analysis_data.RData")
> > ~~~
> > {: .source}
> {: .solution}
{: .challenge}

## Putting It All Together

To assess whether the code upholds the reproducibility standard of being both ***independently understandable*** and ***reusable***, code files must undergo an initial inspection to identify any issues that can make reproducibility difficult or impossible.  The Code Inspection Checklist below outlines the specific tasks involved in a thorough inspection.

> ## Checklist:  Code Inspection 
>
> - Does the code file open and render properly?
> - Does the code include the following components:
>      - Code header metadata
>      - Non-executable comments
>      - Package installation scripts
>      - Data import commands
>      - Variable transformation scripts
>      - Data analysis commands
>      - Log commands
> - Does the code header metadata include all essential information needed to run the analysis (see [Code Header Metadata Checklist]()?
> - Do non-executable comments provide signposts for the analytical steps in the computational workflow?
> - Do data import commands use relative file paths instead of absolute file paths?
> - If the research compendium contains multiple code files, do the filenames indicate the order in which the code files should be executed?
> - If the research compendium contains multiple code files, is there a main file included in the compendium?
{: .checklist}






{% include links.md %}

