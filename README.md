# R-Basics
R Basics for Beginners
### Introduction

This article is useful for people intended to use R as an elementary introduction. My motto here is 'Learning is FUN!' Let's get started with basic introduction of R.

### Downloading and Installing R

The starting point is the R website at www.r-project.org. You have to find the **CRAN(Comprehensive R Archive Network)** link under the Download section. If you click on the CRAN link, you will be shown a list of network servers all over the planet. You can choose https://cran.cnr.berkeley.edu/. Then select the appropriate download for Windows or Mac OS X. For windows users, you have to select **'install R for the first time'** under the base section.The next prompt depends on the browser you are using. I usually use Google Chrome. The download is usually in the lower-left corner of the screen. If using Internet Explorer, select **“Run” Select “Yes”** to allow changes to be made. Select the appropriate prompts for the next few screens. I go with the defaults. After installation is complete, install **RStudio**.

Once you are done with downloading R, you have to go to the link https://www.rstudio.com for installing the free version of RStudio. Scroll to the middle of the page and select **'DOWNLOAD RSTUDIO DESKTOP'** under the column 'Open Source Edition'.

### Help and Question Mark in R

While working on R, we have to keep in mind that we may have various possibilities for a single task. If you want to see the data through a figure we can search for a boxplot. All you have to do is to type '?boxplot' or help(boxplot). A help window opens, showing a document with the headings Description, Usage, Arguments, Details, Values, References, See also, and Examples. www.r-project.org is another important link to start with if you are stuck with any problem.

### Setting Working Directory

The **getwd()** and **setwd()** commands identify the current working directory and sets a new working directory, respectively. To find the deafault working directory you can type getwd().

```{r}
getwd()
```

My current directory is shown above. Another useful command is **q()** for quitting R. It exits R. Before it does so, it will ask whether it should save the workspace. If you decide to save it, we strongly advise that you do not save it in its default directory. Doing so will cause R to load all your results automatically when it is
restarted. To avoid R asking whether it should save your data, use

> q(save = "no")

To save a workspace, click **File-<Save Workspace**. To load an existing workspace, use **File-<Load Workspace**. f you want to begin a new analysis on a different dataset, it may be useful to remove all variables. One option is to quit R and restart it. Alternatively, click **Misc-<Remove all objects**. This will execute the command

```{r}
rm(list = ls(all = TRUE))
```

### Loading Small Data Set

Let's get started! We use a dataset (unpublished data, Chris Elphick, University of Connecticut) containing seven body measurements taken from approximately 1100 saltmarsh sharp-tailed sparrows (Ammodramus caudacutus). For our purposes we use only four morphometric variables of eight birds.

```{r}
#simplest way to store results in each variable
a <- 59
b <- 55
c <- 53.5
d <- 55
e <- 52.5
```

Alternatively, the ‘‘=’’ symbol instead of ‘‘<–’’ can be used. To name your variables, it would be great not to use a,b,c,d. Instead use names related to the data. 

#### Concatenating Data with the c Function

To concatenate data, we can use **c()** function. 

```{r}
#Concatenating Data with the c Function
Wingcrd <- c(59, 55, 53.5, 55, 52.5, 57.5, 53, 55) # c function has created a single vector of length 8
Tarsus <- c(22.3, 19.7, 20.8, 20.3, 20.8, 21.5, 20.6,21.5)
Head <- c(31.2, 30.4, 30.6, 30.3, 30.3, 30.8, 32.5,NA)
Wt <- c(9.5, 13.8, 14.8, 15.2, 15.5, 15.6, 15.6,15.7)

Wingcrd[1] # gives result 59
Wingcrd [1 : 5] #To view the first five values type
Wingcrd [-2] #To view all except the second value
```

Note that there is one bird for which the size of the head was not measured. It is indicated by NA. Depending on the function, the presence of an NA may, or may not, cause trouble. Apparently, the default ‘‘na.rm = FALSE’’ option causes the R function sum to return an NA if there is a missing value in the vector (rm refers to
remove). To avoid this, use "na.rm = TRUE"

```{r}
sum(Head)
sum(Head, na.rm = TRUE)
```

```{r}
#repeat number using 'rep' function
Id <- rep(1 : 4, each = 8)
Id
#repeat numbers using 'seq' function
a <- seq(from = 1, to = 4, by = 1)
rep(a, each = 8)
```

The above chunk repeat the values from 1 to 4, each eight times. You can also use the seq function to generate a sequence.

#### Use of cbind and rbind command

```{r}
#Instead of the c function, we could have used the 'vector' function
Z <- cbind(Wingcrd, Tarsus, Head, Wt)
Z[,1] #data in the first column
Z[1 : 8, 1] # same O/P as before
Z [2,] #second row data

Z[1, 1] # accesses the value of the first bird for Wingcrd
Z[, 2 : 3] #gives all the data for columns 2 and 3
X <- Z[4, 4] #X contains the weight for bird 4
Y <- Z[, 4] # all the Wt data
W <- Z[, -3] # minus sign is used to exclude columns or rows
D <- Z[, c(1, 3, 4)]
E <- Z[, c(-1, -3)]
# if you only need to store the number of rows in Z
zrow <- dim(Z)[1]

Z2 <- rbind(Wingcrd, Tarsus, Head, Wt) # combines the data in rows
```

#### Combining data using matrix function

We can create a matrix of dimension 8 by 4 that contains the data. 

```{r}
##create a matrix of dimension 8 by 4
Dmat <- matrix(nrow = 8, ncol = 4)

Dmat[, 1] <- c(59, 55, 53.5, 55, 52.5, 57.5, 53, 55)
Dmat[, 2] <- c(22.3, 19.7, 20.8, 20.3, 20.8, 21.5,20.6, 21.5)
Dmat[, 3] <- c(31.2, 30.4, 30.6, 30.3, 30.3, 30.8,2.5, NA)
Dmat[, 4] <- c(9.5, 13.8, 14.8, 15.2, 15.5, 15.6,15.6, 15.7)
Dmat
```

The elements of Dmat, in this case, are entered by column, but we could have filled them in by row. Typing Dmat into R gives the same data matrix as we obtained with the cbind function, except that Dmat does not have column labels.

We can use the existing colnames function to add column names to Dmat

```{r}
#use the existing colnames function to add column names to Dmat
colnames(Dmat) <- c("Wingcrd", "Tarsus", "Head","Wt")
Dmat
```

Other useful way to combine data

```{r}
Dmat2 <- as.matrix(cbind(Wingcrd, Tarsus, Head, Wt))
Dmat2
```

Dmat2 and Dmat are identical. Functions such as 'as.matrix', 'is.matrix' (this function gives a TRUE if its argument is a matrix, and FALSE otherwise), as.data.frame, is.date.frame can come in handy

#### Combining Data with the data.frame Function

In a data frame we can combine variables of equal length, with each row in the data frame containing
observations on the same sampling unit. 

```{r}
#'data.frame'is similar to the 'matrix' or 'cbind' functions
Dfrm <- data.frame(WC = Wingcrd,
                   TS = Tarsus,
                   HD = Head,
                   W = Wt)
Dfrm
```

We can use knitr package in R to generate a nice table by Kable function.

```{r}
library(knitr)
kable(Dfrm)
```

Basically, the data.frame function creates an object, called Dfrm in this case, and within Dfrm it stores values of the four morphometric variables. The advantage of a data frame is that you can make changes to the data without affecting the original data.Possible to combine the original weight and the square root transformed weights in the data frame Dfrm.

```{r}
Dfrm2 <- data.frame(WC = Wingcrd,
                   TS = Tarsus,
                   HD = Head,
                   W = Wt,
                   Wsq = sqrt(Wt))
kable(Dfrm2)
```

In the data frame, we can also combine numerical variables, character strings, and factors. 

#### Combining Data Using the list Function

Suppose you want a black box into which you can put as many variables as you want; some may be related, some may have similar dimensions, some may be vectors, others matrices, and yet others may contain character strings of variable names. This is what the list function can do.

```{r}
# 'list' function combines data of different dimensions
x1 <- c(1, 2, 3)
x2 <- c("a", "b", "c", "d")
x3 <- 3
x4 <- matrix(nrow = 2, ncol = 2)
x4[, 1] <- c(1, 2)
x4[, 2] <- c( 3, 4)
Y <- list(x1 = x1, x2 = x2, x3 = x3, x4 = x4)
Y
```

All information contained in Y is accessible by typing, for example, Y$x1, Y$x2, and so on. Nearly all functions (e.g., linear regression, generalised linear modelling, t-test, etc.) in R produce output that is stored in a list.

```{r}
Y$x1 # fetch the data for x1
Y$x2  # fetch the data for x2
```

### Loading Large Data Set

```{r}

#Data Load from Excel 
# The 'header = TRUE' option in the 'read.table' function tells R that the first row contains labels.
Squid <- read.table(file = "/Users/mominul/OneDrive - South Dakota State University - SDSU/Data Science/Books/R Books/A Beginners Guide to R/RBook/squid.txt",header = TRUE)

#Loading Excel File
library(readxl)
Vole_Skulls <- read_excel("/Users/mominul/OneDrive - South Dakota State University - SDSU/STAT 601/Project 1/Vole Skulls.xlsm")

#First 5 rows of the loaded data
head(Vole_Skulls)

#csv data set reading
water <- read.csv('https://umich.instructure.com/files/399172/download?download_frd=1', header=T)
# text file reading, use 'read.delim()' command
colnames(water) # Show column Names

#selecting parts of a data set
wa2 <- water$Year..string.
#selecting multiple columns like 2,4 and 5
wa1 <- water[, c(2, 4, 5)]
#selecting columns from 1 to 5
wa <- water[, c(1:5)]
```

To read text file,  use 'read.delim()' command. 

Let us now discuss a bad way of accessing variables. We have used "$" to access variables from the data frame Squid. It can be tedious typing Squid each time we want to use certain variables from the GSI dataset. It is possible to avoid this by using the attach command.

```{r}
attach(Squid)
#base R Boxplot
boxplot(GSI)
# mean of a certain variable
mean(GSI)
```
If you use the attach command, make sure that you use unique variable names. Refrain from common names such as Month, Location, and the like.

### Subset of the Data

You may face a situation where you only want to work with, for example, the female data, data from a certain location, or data from the females of a certain location. To extract the subsets of data, we need to know how sex was coded.

```{r}
a <- Squid$Sex
head(a)
```

Basically it shows all values in the variable Sex. A better option is to use the unique command that shows how many unique values there are in this variable.


```{r}
unique(Squid$Sex)
```

The 1 stands for male, and the 2 for female. 

```{r}
SquidM <- Squid[Squid$Sex == 1, ] #male data
SquidF <- Squid[Squid$Sex == 2, ] #female data
```

#### Conditional Selection

```{r}
unique(Squid$Location)
```


The **unique** command applied on **Squid$Location** shows that there are four locations coded as 1, 2, 3, and 4. To extract the data from location 1, 2, or 3 we can use the following statements that all give the same result (the | symbol stands for the Boolean **‘‘or’’** and the != for **‘‘not equal’’**).

```{r}
Squid13 <- Squid[Squid$Location == 1 | Squid$Location == 2 | Squid$Location == 3, ] # or symbol
Squid12 <- Squid[Squid$Location != 4, ]
Squid31 <- Squid[Squid$Location < 4, ]
quid123 <- Squid[Squid$Location <= 3, ]
id123 <- Squid[Squid$Location >= 1 & Squid$Location <= 3, ]
```


Next we use the ‘‘&,’’ which is the Boolean ‘‘and’’ operator. Suppose we want to extract the male data from
location 1. This means that the data have to be both from male squid and from location 1. 

```{r}
SquidM.1 <- Squid[Squid$Sex == 1 & Squid$Location == 1,]
dim(Squid) # Dimension of the original Dataset
dim(SquidM.1) #dimension after modification
head(SquidM.1 ) # First Few rows in the data set
```

Use of **and or** in a single line

```{r}
# data from males and from location 1 or 2
male.12 <- Squid[Squid$Sex == 1 & (Squid$Location == 1 | Squid$Location == 2), ]
dim(male.12)
```



