---
title: "Clean File"
author: "Bill Kerneckel, Kyle Killion, Eyal Greenberg"
date: "May 28, 2016"
output: html_document
---

## Clean file for 2011 Brooklyn real estate data
<br>

```{r setup, include=FALSE}

knitr::opts_chunk$set(cache=TRUE)

require(gdata)

require(plyr)

bk <- read.xls("2011_brooklyn.xls",pattern="BOROUGH")
```

#### Step 1 - Perform some basic analysis on the data before we start tidying the data

```{r}
head(bk)
```

```{r}
summary(bk)
```

```{r}
str(bk)
```

<br>


#### Follow the steps below to tidy the data
The steps below will load remove the header data form the file, clean/format the data and remove zero sale price data. 
<br>
<br>

#### Step 1 - Clean and format the data with regular expressions. In this step we will transform the data by changing numeric values to a factor, changing all variables to lower case, remove leading digits, and change formatting of dates.
````````````
Change Sales price from numeric to a factor

bk$SALE.PRICE.N <- as.numeric(gsub("[^[:digit:]]","", bk$SALE.PRICE))
count(is.na(bk$SALE.PRICE.N))


Transform all variables to lower case

names(bk) <- tolower(names(bk)) 


Remove leading digits

bk$gross.sqft <- as.numeric(gsub("[^[:digit:]]","", bk$gross.square.feet))
bk$land.sqft <- as.numeric(gsub("[^[:digit:]]","", bk$land.square.feet))


Change sale.date to a date format in R

bk$sale.date <- as.Date(bk$sale.date)
bk$year.built <- as.numeric(as.character(bk$year.built))
````````````

```{r}
knitr::opts_chunk$set(cache=TRUE)

bk$SALE.PRICE.N <- as.numeric(gsub("[^[:digit:]]","", bk$SALE.PRICE))

count(is.na(bk$SALE.PRICE.N))

names(bk) <- tolower(names(bk)) 

bk$gross.sqft <- as.numeric(gsub("[^[:digit:]]","", bk$gross.square.feet))

bk$land.sqft <- as.numeric(gsub("[^[:digit:]]","", bk$land.square.feet))

bk$sale.date <- as.Date(bk$sale.date)

bk$year.built <- as.numeric(as.character(bk$year.built))
```


