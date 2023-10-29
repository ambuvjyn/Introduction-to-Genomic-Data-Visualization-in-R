---
marp: true
---
# Introduction to Genomic Data Visualization in R

---
## Course Purpose

## The purpose of this course is to provide students with a comprehensive introduction to the field of genomic data visualization using the R programming language.

---

## Genomics is a rapidly evolving and data-rich field, and the ability to effectively visualize and interpret genomic data is crucial for researchers and professionals working in genomics and bioinformatics.

## This course is designed to bridge the gap between genomics and data visualization, equipping students with the skills and knowledge necessary to extract meaningful insights from biological data through the creation and interpretation of various types of plots and graphs.

---

## By the end of this course, students will be able to:

- Develop a strong foundation in R programming
- Create and customize a wide range of **data visualizations**
- Proficiently use **Multidimensional Scaling (MDS)** for visualizing high-dimensional genomic data
- Generate and interpret **volcano plots** and **MA plots**
- Prepare and visualize **Gene Ontology (GO) data**
- Create customized **heat maps** in R

---

## Introduction to R for Bioinformatics

This course will emphasize the practical application of R rather than delving into its theoretical underpinnings. Nevertheless, a solid grasp of programming fundamentals is essential for gaining a deeper insight into R.

---

## R

R is a language and environment for statistical computing and graphics developed in the early 1990s. It provides a wide variety of statistical and graphical techniques, including linear and nonlinear modeling, statistical tests, time series analysis, classification, and clustering, among many others.

---

### R:

 - Is free!
 - Is open source and highly extensible, meaning that the user community can (and does) write new R tools
 - Makes publication quality figures, including mathematical symbols and formulae
 - Compiles and runs on Windows, MacOS, and a wide variety of UNIX and Linux systems
 - Has a large and active user community

There are many ways to use R: from the command line, from a script, or in a graphical interface, like RStudio.

---

## RStudio

RStudio is an integrated development environment (IDE), which offers:

 - Syntax highlighting
 - Code completion
 - Smart indentation
 - Workspace browser
 - Data viewer
 - Embedded plots
 - Notebooks that generate PDF or HTML results
 - Package management

---

### R Team Packages

The team behind RStudio are also the authors of a suite of R packages for data science and visualization collectively known as the “tidyverse.” We will be using their extremely popular plotting package, ggplot2, as well as a few other packages from the tidyverse suite later in this course.

---

## RStudio and R notebooks

> **Launch RStudio**

## 1.1 RStudio

As mentioned above, RStudio is a very nice, but optional, IDE for R. All of the code for this course will work just as well on the command line, but RStudio provides a number of features that improve the experience of learning to the basics of R.

---

Your RStudio window should look something like this:

![Rstudio IDE](/assets/images/rstudio.png)

---

## 1.1.1 The console

On the left hand side is the console. This is a command-line interface for R; you type a command, press enter to run it, and the result will appear below.

![Console IDE](/assets/images/console.png)

---

### Running a simple command

In R the prompt is a > character. When you see this character at the beginning of the line in your console, it means that R is waiting for you to type your next command.

In this course, code is going to appear in gray boxes, like this:

`1 + 1`

Whenever you see one of these boxes, try running the code yourself.

What happens if you press enter before you meant to?

`1 + `

---
### Running incomplete command

![Console IDE](/assets/images/console2.png)

If you press enter before finishing a command, the next line will begin with a + character. This lets you know that R is expecting more input.

---

## 1.1.2 The workspace browser

In the upper right panel is the workspace (or environment) browser. This part of the window shows the objects present in the environment. Currently there are none.

The easiest way to explain an object is to run some code.

`a <- 1 + 1`

Unlike the first time we ran 1 + 1, nothing is printed to the console.

Instead, a new value appears in the workspace browser.

---

![Console IDE](/assets/images/console3.png)

![Console IDE](/assets/images/environment.png)

---

The *<-* is a special pair of characters called the assignment operator that stores the result of the addition in the object referred to on the left-hand side of the “arrow.”

Since no object called “a” existed in R’s environment, R created a new object “a” to hold the result of the addition operation 1 + 1.

![Console IDE](/assets/images/environment2.png)

---

## 1.1.3 Help documentation

The lower right pane contains the file browser, plot viewer, and help documentation, which we will be using frequently.

![Console IDE](/assets/images/help.png)

---

## 2 Importing and exporting data

For the remainder of this course, we will be working with a single data set to answer a number of simple biological questions about the effects of maternal cigarrette use during pregnancy. 

Begin by setting up a working directory for this course.

To make things easier, we’ll set R’s working directory to the directory named "workshop". To do this, select the “Session” menu in the toolbar, then navigate to “Set Working Directory,” and click on “Choose Directory.” Choose the "worksop" directory.

---

When you do so, you should see that a line of code ran in your console:

`setwd("D:/Users/ambuv/Desktop/workshop")`

_file names change based on individual systems_

### Download the data.

`download.file("https://raw.githubusercontent.com/ucdavis-bioinformatics-training/2022_February_Introduction_to_R_for_Bioinformatics/main/birthweight.csv", "birthweight.csv")`

---

## 2.1 Import data using read.csv()

R has a number of functions for reading data in a variety of formats. Let’s use the read.csv() function to read in a spreadsheet containing data from an experiment.

`birthweight <- read.csv("birthweight.csv")`

CSV stands for “comma separated value,” and the CSV file is simply a text file where each row in the file represents a row in the data table, and the columns are separated by commas. The contents of the CSV file are now stored in the variable “birthweight.”

---

## 2.2 Export data using write.csv()

To write the contents of the birthweight object to a new CSV, we can use the write.csv() function.

`write.csv(birthweight, file = "new_birthweight.csv")`

The similar `read.delim()` and `write.delim()` can be used to read and write tab-delimited files, where columns are separated by tab characters rather than commas.

---

