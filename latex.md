Introduction to LaTeX
======================================================================================
A brief introduction using an example document
------------------------------------------------------

Chris Paciorek, Department of Statistics, UC Berkeley



# 0) This Tutorial

This tutorial covers the basics of LaTeX, which is widely used in scientific and academic contexts to prepare documents. LaTeX is particularly good at handling mathematical notation and LaTeX syntax for specifying math can be embedded in a wide variety of contexts (Jupyter/IPython Notebook, R Markdown, Microsoft Word equation editor, etc.). Here we'll briefly discuss the use of LaTeX for standalone documents, as a way to get started with using LaTeX syntax more generally.

A screencast accompanies this material.

We'll use a virtual machine developed here at Berkeley, [the Berkeley Common Environment (BCE)](http://bce.berkeley.edu). BCE is a virtual Linux machine - basically it is a Linux computer that you can run within your own computer, regardless of whether you are using Windows, Mac, or Linux. This provides a common environment so that things behave the same for all of us.

Materials for this tutorial, including the R markdown file that was used to create this document are available on github at (https://github.com/berkeley-scf/tutorial-dynamic-docs).  You can download the files by doing a git clone from a terminal window on UNIX-like machine. The following will work from the command line on BCE.

```bash
git clone https://github.com/berkeley-scf/tutorial-dynamic-docs
```

To create this HTML document, simply compile the corresponding R Markdown file in R as follows (the following will work from within BCE after cloning the repository as above).

```bash
Rscript -e "library(knitr); knit2html('latex.Rmd')"
```

<!--
#pandoc --number-sections spark.md -o spark.html
#Rscript -e "library(knitr); knit('spark.Rmd')"
#pandoc --mathjax --number-sections spark.md -o spark.html
-->



# 1) Getting prepared

First, you'll need to get the BCE virtual machine running on your computer. Start by installing the VirtualBox software on your local machine. BCE runs on VirtualBox. Please follow the [BCE installation instructions](http://bce.berkeley.edu/install). Once you've done this, you'll have a Linux computer running within your own machine.

That said, if you'd like to work on your own machine, you can. But you'll need to install LaTeX.

# 2) The LaTeX document format

LaTeX allows you to do essentially anything in a document, including math syntax, including tables and figures, adding a bibliography, including a table of contents, etc. 

The basic premise of LaTeX, in contrast to Word, is that it is a markup language for defining your document. It's NOT a what-you-see-is-what-you-get (WYSIWYG) program. Rather than specifying the exact formatting of a given word, line, or paragraph, you specify what kind of object everything is and LaTeX deals with the formatting. You do this in a plain text document using LaTeX syntax. 

That said, you can monkey with the formatting of individual pieces of your document, as well as monkeying with the formatting of the entire document.

This is not meant as an in-depth introduction to LaTeX, but rather to get you going quickly based on an example, so let's dive into that.

## 2.1) Basic LaTeX syntax

The file *demo_paper.tex* provides an example LaTeX document. The material is taken from a scientific paper but includes only bits and pieces and is not meant to actually be read. Rather it illustrates a lot of the syntax of LaTeX. 

Look through the document and note the following:

* The *preamble* (the part before `\begin{document}`), which sets up the document.
* The commands for defining sections and subsections. 
* The use of user-defined macros (see `\newcommand`) to define commonly-used syntax that can be used anywhere in the document.
* The specification of math syntax in so-called *math mode*, which is done inside special symbols (`\begin{eqnarray}`, `$`, and `\[`, among others). 
* The insertion of figures and tables. LaTeX will figure out where to put them.
* The use of `\label{sec:methods}` and `\ref{sec:methods}` to define and refer to sections, tables, and figures. LaTeX will figure out the numbering for you.
* The inclusion of a bibliography using BibTeX with `\bibliography{name_of_file_with_refs.bib}`, whose style can be specified with `\bibliographystyle`. 

## 2.2) Additional functionality for LaTeX

There is a huge variety of add-on packages for LaTeX that provide additional functionality. These are generally provided as *style* files whose names end in .sty. To use a package, you use the `\usepackage` command. The corresponding .sty file should generally be in the directory in which you are working or in a standard location on your machine. For example there is a line numbering package provided in *lineno.sty* that will allow you to add line numbers to your document as follows:
```
% load the package and specify the left option to put linenumbers on the left side of the page
\usepackage[left]{lineno}  
% enable line numbering in your document
\linenumbers               
```

In addition, there is a wide variety of classes that format your document in a pre-specified way, such as for particular academic journals. To use a class, you use the `\documentclass{}` syntax. The classes are provided by class files whose names end in .cls. The *article* class (`\documentclass{article}`) is a standard class that comes with LaTeX. 

Related to this, there is a wide variety of biblography styles available via .bst files.

# 3) Compiling LaTeX to PDF and other formats

The standard way to create a document from a LaTeX file is to create a PDF using `pdflatex`.  There are also ways to create HTML from LaTeX and to convert from LaTeX to other formats (e.g., see `pandoc`). Here we'll just see the creation of a PDF, including use of a bibliography. In general you'll need to run `pdflatex` multiple times as there are multiple layers of processing.


```bash
pdflatex demo_paper
bibtex demo_paper    # to create the bibliography file (.bbl)
pdflatex demo_paper  # to get the cross-referencing and numbering right
pdflatex demo_paper  # to get the bibliography and refs right
```

`bibtex` creates the bibliography file (.bbl) specific to this document from one or more .bib files (which are basically a database of references and can include references not used in the document) and the bibliography style file (.bst). 

# 4) Other resources

In addition to a wide variety of resources available via Googling...

* Point to our knitr/dynamic documents and pandoc and Jupyter tutorials
* You might look at www.latex-tutorial.com for tutorial info. 
* There are many good books on LaTeX, including *LaTeX, A Document Preparation System* by Leslie Lamport and others listed [here](http://latex-project.org/guides/books.html).
* Phil Spector formerly of the UCB Statistics Department, has a nice (albeit a bit old) [overview](https://www.stat.berkeley.edu/~spector/latex2e.pdf).
