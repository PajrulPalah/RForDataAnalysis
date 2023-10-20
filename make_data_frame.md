---
title: "Create your own data frame"
output: html_document
---

## Background for this activity
This activity is focused on creating and using data frames in `R`. A data frame is a collection of columns containing data, similar to a spreadsheet or SQL table. Data frames are one of the basic tools you will use to work with data in `R`. And you can create data frames from different data sources.  

There are three common sources for data:

- A`package` with data that can be accessed by loading that `package`
- An external file like a spreadsheet or CSV that can be imported into `R`
- Data that has been generated from scratch using `R` code

Wherever data comes from, you will almost always want to store it in a data frame object to work with it. Now, you can start creating and exploring data frames with the code chunks in the RMD space. To interact with the code chunk, click the green arrow in the top-right corner of the chunk. The executed code will appear in the RMD space and your console.

Throughout this activity, you will also have the opportunity to practice writing your own code by making changes to the code chunks yourself. If you encounter an error or get stuck, you can always check the Lesson2_Dataframe_Solutions .rmd file in the Solutions folder under Week 3 for the complete, correct code.

## Step 1: Load packages

Start by installing the required package; in this case, you will want to install `tidyverse`. If you have already installed and loaded `tidyverse` in this session, feel free to skip the code chunks in this step.

```{r}
install.packages("tidyverse")
```

Once a package is installed, you can load it by running the `library()` function with the package name inside the parentheses:

```{r}
library(tidyverse)
```

## Step 2: Create data frame

Sometimes you will need to generate a data frame directly in `R`. There are a number of ways to do this; one of the most common is to create individual vectors of data and then combine them into a data frame using the `data.frame()` function.

Here's how this works. First, create a vector of names by inserting four names into this code block between the quotation marks and then run it:

```{r}
names <- c("sarjut", "Iben", "Usep", "sarkonji")
```

Then create a vector of ages by adding four ages separated by commas to the code chunk below. Make sure you are inputting numeric values for the ages or you might get an error. 

```{r}
age <- c(20, 30, 60, 70)
```

With these two vectors, you can create a new data frame called `people`:

```{r}
people <- data.frame(names, age)
```

## Step 3: inspect the data frame

Now that you have this data frame, you can use some different functions to inspect it.

One common function you can use to preview the data is the `head()` function, which returns the columns and the first several rows of data. You can check out how the `head()` function works by running the chunk below:

```{r}
head(people)
```

In addition to `head()`, there are a number of other useful functions to summarize or preview your data. For example, the `str()` and `glimpse()` functions will both provide summaries of each column in your data arranged horizontally. You can check out these two functions in action by running the code chunks below:

```{r}
str(people)
```

```{r}
glimpse(people)
```

You can also use `colnames()` to get a list the column names in your data set. Run the code chunk below to check out this function:

```{r}
colnames(people)
```

Now that you have a data frame, you can work with it using all of the tools in `R`. For example, you could use `mutate()` if you wanted to create a new variable that would capture each person's age in twenty years. The code chunk below creates that new variable:

```{r}
mutate(people, age_in_20 = age + 20)
```