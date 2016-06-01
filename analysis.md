---
title: "Analysis"
author: "Bill Kerneckel, Kyle Killion, Eyal Greenberg"
date: "May 28, 2016"
output: html_document
---

## Analysis for 2011 Brooklyn real estate data

```{r setup2, include=FALSE}

knitr::opts_chunk$set(cache=TRUE)

require(gdata)

require(plyr)

bk <- read.xls("2011_brooklyn.xls",pattern="BOROUGH")
```
```{r setup3, include=FALSE}
knitr::opts_chunk$set(cache=TRUE)

bk$SALE.PRICE.N <- as.numeric(gsub("[^[:digit:]]","", bk$SALE.PRICE))

count(is.na(bk$SALE.PRICE.N))

names(bk) <- tolower(names(bk)) 

bk$gross.sqft <- as.numeric(gsub("[^[:digit:]]","", bk$gross.square.feet))

bk$land.sqft <- as.numeric(gsub("[^[:digit:]]","", bk$land.square.feet))

bk$sale.date <- as.Date(bk$sale.date)

bk$year.built <- as.numeric(as.character(bk$year.built))
```

#### Step 1 - Analysis the sales and square footage data. We need to make sure sales price is correct.
`````````````
attach(bk)
hist(sale.price.n) # Something weird here
hist(sale.price.n[sale.price.n>0])
hist(gross.sqft[sale.price.n==0])
detach(bk)
`````````````

```{r}
knitr::opts_chunk$set(cache=TRUE)

attach(bk)
hist(sale.price.n)
hist(sale.price.n[sale.price.n>0])
hist(gross.sqft[sale.price.n==0])
detach(bk)
```

<br>

#### Step 2 - From the analysis above we need to only keep the actual sales data
`````````````
bk.sale <- bk[bk$sale.price.n!=0,]
plot(bk.sale$gross.sqft,bk.sale$sale.price.n)
plot(log10(bk.sale$gross.sqft),log10(bk.sale$sale.price.n))
`````````````
<br>

```{r}
knitr::opts_chunk$set(cache=TRUE)

bk.sale <- bk[bk$sale.price.n!=0,]
plot(bk.sale$gross.sqft,bk.sale$sale.price.n)
plot(log10(bk.sale$gross.sqft),log10(bk.sale$sale.price.n))
```

<br>

#### Step 3 - Keep only the actual sales 
`````````````
bk.sale <- bk[bk$sale.price.n!=0,]
plot(bk.sale$gross.sqft,bk.sale$sale.price.n)
plot(log(bk.sale$gross.sqft),log(bk.sale$sale.price.n))
`````````````
<br>

```{r}
bk.sale <- bk[bk$sale.price.n!=0,]
plot(bk.sale$gross.sqft,bk.sale$sale.price.n)
plot(log(bk.sale$gross.sqft),log(bk.sale$sale.price.n))
```


#### Step 4 - For now, let's look at 1-, 2-, and 3-family homes
`````````````
bk.homes <- bk.sale[which(grepl("FAMILY",bk.sale$building.class.category)),]
dim(bk.homes)
plot(log(bk.homes$gross.sqft),log(bk.homes$sale.price.n))
summary(bk.homes[which(bk.homes$sale.price.n<100000),])
`````````````
<br>

```{r}
knitr::opts_chunk$set(cache=TRUE)

bk.homes <- bk.sale[which(grepl("FAMILY",bk.sale$building.class.category)),]
dim(bk.homes)
plot(log(bk.homes$gross.sqft),log(bk.homes$sale.price.n))
summary(bk.homes[which(bk.homes$sale.price.n<100000),])
```

<br>

#### Step 5 - Finally lets remove any outliers that weren't actual sales
`````````````
bk.homes$outliers <- (log10(bk.homes$sale.price.n) <=5) + 0
bk.homes <- bk.homes[which(bk.homes$outliers==0),]
plot(log(bk.homes$gross.sqft),log(bk.homes$sale.price.n))
`````````````
<br>

```{r}
knitr::opts_chunk$set(cache=TRUE)

bk.homes$outliers <- (log10(bk.homes$sale.price.n) <=5) + 0
bk.homes <- bk.homes[which(bk.homes$outliers==0),]
plot(log(bk.homes$gross.sqft),log(bk.homes$sale.price.n))
```