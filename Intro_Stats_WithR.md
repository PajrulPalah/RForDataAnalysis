
# Introduction to R and RStudio with Statsr

## Introduction

The goal of this lab is to introduce you to R and RStudio, which you'll be using
throughout the course both to learn the statistical concepts discussed in the 
course and to analyze real data and come to informed conclusions. To straighten 
out which is which: R is the name of the programming language itself and RStudio 
is a convenient interface.

As the labs progress, you are encouraged to explore beyond what the labs dictate;
a willingness to experiment will make you a much better programmer. Before we 
get to that stage, however, you need to build some basic fluency in R. Today we
begin with the fundamental building blocks of R and RStudio: the interface, 
reading in data, and basic commands.

## RStudio

Your RStudio window has four panels.

The panel on the lower left is where the action happens. It's called the *console*. 
Everytime you launch RStudio, it will have the same text at the top of the 
console telling you the version of R that you're running. Below that information
is the *prompt*. As its name suggests, this prompt is really a request, a 
request for a command. Initially, interacting with R is all about typing commands
and interpreting the output. These commands and their syntax have evolved over
decades (literally) and now provide what many users feel is a fairly natural way
to access data and organize, describe, and invoke statistical computations.

The panel in the upper right contains your *workspace* as well as a history of 
the commands that you've previously entered. 

Any plots that you generate will show up in the panel in the lower right corner. 
This is also where you can browse your files, access help, manage packages, etc.


## R Packages

R is an open-source programming language, meaning that users can contribute
packages that make our lives easier, and we can use them for free. For this lab,
and many others in the future, we will use the following R packages:

- `statsr`: for data files and functions used in this course
- `dplyr`: for data wrangling
- `ggplot2`: for data visualization

You should have already installed these packages using commands like 
`install.packages` and `install_github`.

Next, you need to load the packages in your working environment. We do this with
the `library` function. Note that you only need to **install** packages once, but
you need to **load** them each time you relaunch RStudio.

```{r load-packages, message = FALSE}
library(dplyr)
library(ggplot2)
library(statsr)
```

To do so, you can 

- click on the green arrow at the top of the code chunk in the R Markdown (Rmd) 
file, or
- highlight these lines, and hit the **Run** button on the upper right corner of the 
pane, or
- type the code in the console.

Going forward you will be asked to load any relevant packages at the beginning
of each lab.

## Dataset 1: Dr. Arbuthnot's Baptism Records

To get you started, run the following command to load the data.

```{r load-abrbuthnot-data}
data(arbuthnot)
```

To do so, once again, you can 

- click on the green arrow at the top of the code chunk in the R Markdown (Rmd) 
file, or
- put your cursor on this line, and hit the **Run** button on the upper right 
corner of the pane, or
- type the code in the console.

This command instructs R to load some data. The Arbuthnot baptism counts for boys 
and girls. You should see that the workspace area in the upper righthand corner of 
the RStudio window now lists a data set called `arbuthnot` that has 82 observations 
on 3 variables. As you interact with R, you will create a series of objects. 
Sometimes you load them as we have done here, and sometimes you create them yourself 
as the byproduct of a computation or some analysis you have performed.

The Arbuthnot data set refers to Dr. John Arbuthnot, an 18<sup>th</sup> century 
physician, writer, and mathematician. He was interested in the ratio of newborn
boys to newborn girls, so he gathered the baptism records for children born in
London for every year from 1629 to 1710. We can take a look at the data by 
typing its name into the console.

```{r view-data}
arbuthnot
```
The result

![WhatsApp Image 2023-09-13 at 09 18 35](https://github.com/PajrulPalah/Basic_R_For_Data-Analysis/assets/143974279/9b9b6be9-1722-4f98-9bd6-00436a0ee04e)

However printing the whole dataset in the console is not that useful. 
One advantage of RStudio is that it comes with a built-in data viewer. Click on
the name `arbuthnot` in the *Environment* pane (upper right window) that lists 
the objects in your workspace. This will bring up an alternative display of the 
data set in the *Data Viewer* (upper left window). You can close the data viewer
by clicking on the *x* in the upper lefthand corner.

What you should see are four columns of numbers, each row representing a 
different year: the first entry in each row is simply the row number (an index 
we can use to access the data from individual years if we want), the second is 
the year, and the third and fourth are the numbers of boys and girls baptized 
that year, respectively. Use the scrollbar on the right side of the console 
window to examine the complete data set.

Note that the row numbers in the first column are not part of Arbuthnot's data. 
R adds them as part of its printout to help you make visual comparisons. You can
think of them as the index that you see on the left side of a spreadsheet. In 
fact, the comparison to a spreadsheet will generally be helpful. R has stored 
Arbuthnot's data in a kind of spreadsheet or table called a *data frame*.

You can see the dimensions of this data frame by typing:

```{r dim-data}
dim(arbuthnot)
```
The result

![WhatsApp Image 2023-09-13 at 09 57 25](https://github.com/PajrulPalah/Basic_R_For_Data-Analysis/assets/143974279/8c80ef7d-a49d-4df0-ad8c-493b95d88418)

This command should output `[1] 82 3`, indicating that there are 82 rows and 3 
columns (we'll get to what the `[1]` means in a bit), just as it says next to 
the object in your workspace. You can see the names of these columns (or 
variables) by typing:

```{r names-data}
names(arbuthnot)
```
The Result

![WhatsApp Image 2023-09-13 at 10 08 12](https://github.com/PajrulPalah/Basic_R_For_Data-Analysis/assets/143974279/40dcf4fb-7993-4916-89a5-14464ed92bec)


You should see that the data frame contains the columns `year`,  `boys`, and 
`girls`. At this point, you might notice that many of the commands in R look a 
lot like functions from math class; that is, invoking R commands means supplying
a function with some number of arguments. The `dim` and `names` commands, for 
example, each took a single argument, the name of a data frame.

<div class="boxedtext">
**Tip: ** If you use the up and down arrow keys, you can scroll through your 
previous commands, your so-called command history. You can also access it 
by clicking on the history tab in the upper right panel. This will save 
you a lot of typing in the future.
</div>

### R Markdown

So far we asked you to type your commands in the console. The console is a great 
place for playing around with some code, however it is not a good place for 
documenting your work. Working in the console exclusively makes it difficult to 
document your work as you go, and reproduce it later. 

R Markdown is a great solution for this problem. And, you already have worked with 
an R Markdown document -- this lab! Going forward type the code for the questions 
in the code chunks provided in the R Markdown (Rmd) document for the lab, and **Knit**
the document to see the results.

### Some Exploration

Let's start to examine the data a little more closely. We can access the data in
a single column of a data frame separately using a command like

```{r view-boys}
arbuthnot$boys
```
The result

![WhatsApp Image 2023-09-13 at 09 57 46](https://github.com/PajrulPalah/Basic_R_For_Data-Analysis/assets/143974279/9abc91ca-6052-4fba-bdca-401f68807af1)


Notice that the way R has printed these data is different. When we looked at the
complete data frame, we saw 82 rows, one on each line of the display. These data
are no longer structured in a table with other variables, so they are displayed 
one right after another. Objects that print out in this way are called vectors; 
they represent a set of numbers. R has added numbers in [brackets] along the left
side of the printout to indicate locations within the vector. For example, 5218 
follows [1], indicating that 5218 is the first entry in the vector. And if [43] 
starts a line, then that would mean the first number on that line would represent
the 43rd entry in the vector.

R has some powerful functions for making graphics. We can create a simple plot 
of the number of girls baptized per year with the command

```{r plot-girls-vs-year}
ggplot(data = arbuthnot, aes(x = year, y = girls)) +
  geom_point()
```
The result

![WhatsApp Image 2023-09-13 at 09 58 13](https://github.com/PajrulPalah/Basic_R_For_Data-Analysis/assets/143974279/1cf1b1f3-9411-40b4-a29e-4c1e06ca5d10)

Back to the code... We use the `ggplot()` function to build plots. If you run the 
plotting code in your console, you should see the plot appear under the *Plots* tab 
of the lower right panel of RStudio. Notice that the command above again looks like 
a function, this time with arguments separated by commas. 

- The first argument is always the dataset. 
- Next, we provide thevariables from the dataset to be assigned to `aes`thetic 
elements of the plot, e.g. the x and the y axes. 
- Finally, we use another layer, separated by a `+` to specify the `geom`etric 
object for the plot. Since we want to scatterplot, we use `geom_point`.

You might wonder how you are supposed to know the syntax for the `ggplot` function. 
Thankfully, R documents all of its functions extensively. To read what a function 
does and learn the arguments that are available to you, just type in a question mark 
followed by the name of the function that you're interested in. Try the following in
your console:

```{r plot-help, tidy = FALSE}
?ggplot
```

Notice that the help file replaces the plot in the lower right panel. You can 
toggle between plots and help files using the tabs at the top of that panel. 

<div class="boxedtext">
More extensive help for plotting with the `ggplot2` package can be found at 
http://docs.ggplot2.org/current/. The best (and easiest) way to learn the syntax is 
to take a look at the sample plots provided on that page, and modify the code 
bit by bit until you get achieve the plot you want.
</div>

### R as a big calculator

Now, suppose we want to plot the total number of baptisms. To compute this, we 
could use the fact that R is really just a big calculator. We can type in 
mathematical expressions like

```{r calc-total-bapt-numbers}
5218 + 4683
```
The result

![WhatsApp Image 2023-09-13 at 09 58 32](https://github.com/PajrulPalah/Basic_R_For_Data-Analysis/assets/143974279/a9c5f4d6-3b5c-492b-9b05-013cbf86863c)

to see the total number of baptisms in 1629. We could repeat this once for each 
year, but there is a faster way. If we add the vector for baptisms for boys to 
that of girls, R will compute all sums simultaneously.

```{r calc-total-bapt-vars}
arbuthnot$boys + arbuthnot$girls
```
The result

![WhatsApp Image 2023-09-13 at 09 58 47](https://github.com/PajrulPalah/Basic_R_For_Data-Analysis/assets/143974279/a0781c11-a38a-4257-97ff-40296d739ade)

What you will see are 82 numbers (in that packed display, because we aren’t 
looking at a data frame here), each one representing the sum we’re after. Take a
look at a few of them and verify that they are right.

### Adding a new variable to the data frame

We'll be using this new vector to generate some plots, so we'll want to save it 
as a permanent column in our data frame.

```{r calc-total-bapt-vars-save}
arbuthnot <- arbuthnot %>%
  mutate(total = boys + girls)
```

What in the world is going on here? The `%>%` operator is called the **piping** 
operator. Basically, it takes the output of the current line and pipes it into 
the following line of code.

<div class="boxedtext">
**A note on piping: ** Note that we can read these three lines of code as the following: 

*"Take the `arbuthnot` dataset and **pipe** it into the `mutate` function. 
Using this mutate a new variable called `total` that is the sum of the variables
called `boys` and `girls`. Then assign this new resulting dataset to the object
called `arbuthnot`, i.e. overwrite the old `arbuthnot` dataset with the new one
containing the new variable."*

This is essentially equivalent to going through each row and adding up the boys 
and girls counts for that year and recording that value in a new column called
total.
</div>

<div class="boxedtext">
**Where is the new variable? ** When you make changes to variables in your dataset, 
click on the name of the dataset again to update it in the data viewer.
</div>

You'll see that there is now a new column called `total` that has been tacked on
to the data frame. The special symbol `<-` performs an *assignment*, taking the 
output of one line of code and saving it into an object in your workspace. In 
this case, you already have an object called `arbuthnot`, so this command updates
that data set with the new mutated column.

We can make a plot of the total number of baptisms per year with the following command.

```{r plot-total-vs-year-line}
ggplot(data = arbuthnot, aes(x = year, y = total)) +
  geom_line()
```
The result

![WhatsApp Image 2023-09-13 at 09 59 18](https://github.com/PajrulPalah/Basic_R_For_Data-Analysis/assets/143974279/ed04b50b-9f00-4022-aea6-e9b0ca38e93c)

Note that using `geom_line()` instead of `geom_point()` results in a line plot instead
of a scatter plot. You want both? Just layer them on:

```{r plot-total-vs-year-line-and-point}
ggplot(data = arbuthnot, aes(x = year, y = total)) +
  geom_line() +
  geom_point()
```
The result

![WhatsApp Image 2023-09-13 at 09 59 45](https://github.com/PajrulPalah/Basic_R_For_Data-Analysis/assets/143974279/abc6310f-5d01-4280-8928-e167b1afb709)

Finally, in addition to simple mathematical operators like subtraction and 
division, you can ask R to make comparisons like greater than, `>`, less than,
`<`, and equality, `==`. For example, we can ask if boys outnumber girls in each 
year with the expression

```{r boys-more-than-girls}
arbuthnot <- arbuthnot %>%
  mutate(more_boys = boys > girls)
arbuthnot
```
The result

![WhatsApp Image 2023-09-13 at 10 01 20](https://github.com/PajrulPalah/Basic_R_For_Data-Analysis/assets/143974279/8af2b739-d567-402f-b02e-2c5a1ccbc52a)


This command add a new variable to the `arbuthnot` data frame containing the values
of either `TRUE` if that year had more boys than girls, or `FALSE` if that year 
did not (the answer may surprise you). This variable contains different kind of 
data than we have considered so far. All other columns in the `arbuthnot` data 
frame have values are numerical (the year, the number of boys and girls). Here, 
we've asked R to create *logical* data, data where the values are either `TRUE` 
or `FALSE`. In general, data analysis will involve many different kinds of data 
types, and one reason for using R is that it is able to represent and compute 
with many of them.
