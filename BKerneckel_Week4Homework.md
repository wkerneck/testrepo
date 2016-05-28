# 2016-0509 MSDS 6304 Week 4 Homework
Bill Kerneckel  
May 27, 2016  
<br>
<br>
<strong><u>Assignment:</u></strong><br>

Write bootstrap code to illustrate the central limit theorem in R markdown and push the result to GitHub. Use a <strong>normal distribution</strong> with two different sample sizes and an <strong>exponential distribution</strong> with two different sample sizes. Please also comment on the code and explain the results. 

------------
<br>
<strong>Step 1:</strong> Generate normal distribution with two different sample sizes
<br>

```r
x <- rnorm(50, 22, 5)
y <- rnorm(50,25,5)
x1 <- c(x)
y2 <- c(y)
z <- c(x1,y2)
```
<br>
<strong>Step 2:</strong> Now lets output the combined 'z' sample size to see if our above statements worked.
<br>

```r
z
```

```
##   [1] 21.84916 18.57006 18.77559 20.74097 27.49587 22.05086 28.12590
##   [8] 21.33476 20.67847 24.55994 20.32757 23.01282 26.49773 16.70620
##  [15] 18.67368 25.51405 27.34219 19.33712 20.47627 13.70440 19.46164
##  [22] 31.63035 11.41902 20.57065 25.05214 19.07718 20.20722 24.83785
##  [29] 25.37723 23.22028 16.68398 21.69811 13.55011 32.90328 12.95383
##  [36] 24.04454 22.52759 24.23100 18.48801 17.37338 22.43398 21.16476
##  [43] 27.11843 17.97372 19.78132 33.06067 16.85437 20.30153 18.40073
##  [50] 17.79046 25.13301 23.59923 28.09183 18.83797 15.31226 19.54740
##  [57] 19.11135 21.47518 24.29634 23.23996 26.02476 21.85864 28.77752
##  [64] 27.11134 24.96130 29.01494 24.02312 26.93046 20.67566 13.34487
##  [71] 23.22220 25.23223 13.47302 19.97629 18.96391 31.03904 19.77270
##  [78] 17.21730 26.13405 22.47057 24.84641 24.83558 21.65914 27.59382
##  [85] 25.32658 40.11494 25.84882 30.21056 28.16898 26.66676 30.41397
##  [92] 26.70349 25.09957 18.35274 30.16555 21.38953 21.03124 28.64596
##  [99] 27.67951 17.48510
```
<br>
<strong>Step 3:</strong> Lets take the mean of the 'z' sample size.
<br>

```r
zbar <- mean(z)
zbar
```

```
## [1] 22.77068
```
<br>

<strong>Step 4:</strong> Lets apply the bootstrap principal to illustrate the centeral limit theorem. First we need to set the repetitions to 1000.
<br>

```r
nsims <- 1000
```
<br>
<strong>Step 5:</strong> Now we need to loop 1000 repetitions through the combined 'z' sample size of 100. In the loop the following occurs:
  
1. Pulls one value from the 'z' sample size
2. Puts the one value back into the orginal 'z' sample population
3. Calculates 1000 means
<br>
<br>

```r
bootnorm <- numeric(nsims)
 	for (i in 1:nsims) {
	temp <- sample (z, 100, replace=TRUE)
	bootnorm[i] <- mean(temp)
 	}
```
<br>
<strong>Step 6:</strong> Lets see the summary of the bootstrap simulation.
<br>

```r
summary(bootnorm)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   21.32   22.43   22.74   22.75   23.07   24.32
```
<br>

<strong>Step 7:</strong> Now we can compare the bootstrap mean to the orginal mean of the 'z' sample size. You notice how close they are of being equal to each other. Lets compare the standard deviations of the orginal 'z' sample and of the bootstrap data.
<br>
<br>
'z' Sample Standard Deviation<br>

```r
sd(z)
```

```
## [1] 4.988674
```

<br>
Bootnorm Sample Standard Deviation<br>
<br>

```r
sd(bootnorm)
```

```
## [1] 0.4793547
```
<br>

<strong>Step 8:</strong> If we take the standard deviation of the orginal 'z' samples size and divide it by the square root of the 'z' sample size off 100 the results should be the same as the orginal standard deviation of the 'z' sample. By comparing the two demostrates the central limit theorem.
<br>

```r
sd(z)/sqrt(100)
```

```
## [1] 0.4988674
```
<br>

<hr>
<p>The next part of the home work assignment was to demostrate using a exponential distribution with two different sample sizes.</p>
<br>
<br>
<strong>Step 1:</strong> Generate normal distribution with two different sample sizes
<br>

```r
d <- rnorm(50, 22, 5)
e <- rnorm(50,25,5)
d1 <- c(d)
e2 <- c(e)
f <- c(d1,e2)
```
<br>
<strong>Step 2:</strong> Now lets output the combined 'f' sample size to see if our above statements worked:
<br>

```r
f
```

```
##   [1] 21.145835 18.802620 20.446059 26.804646 17.555269 26.619353 22.454334
##   [8] 30.456948 19.736210 19.519892 12.971467 19.625310 19.528427 22.941174
##  [15] 20.037173 27.541465 14.655628 18.658188 22.670925 27.385081 17.283560
##  [22] 14.697469 29.616436 28.706700 21.667875 18.696544 20.000455 17.790708
##  [29] 21.934644 26.533896 11.332926 23.870614 25.949626 27.136045 22.362711
##  [36] 19.615210 11.966863 22.010595 18.290175 31.311242 28.744318 20.136924
##  [43] 15.102249 15.980098 16.466280 17.731082 20.426682  8.926442 14.447301
##  [50] 18.745329 32.837680 28.453037 14.594232 18.747692 26.645473 17.283196
##  [57] 24.431559 25.889158 31.848025 23.806063 32.821286 29.880378 24.549954
##  [64] 16.653397 19.930918 25.329394 26.696158 21.006482 21.799870 21.310416
##  [71] 19.209428 36.172601 26.906118 22.094910 26.877625 18.251643 26.711913
##  [78] 25.798889 23.958049 21.409178 24.809602 22.270610 21.923120 20.468764
##  [85] 34.006425 30.062426 32.027179 19.656925 24.616165 14.769184 23.757592
##  [92] 26.368121 24.409401 22.310693 16.338228 24.989476 15.483375 17.712771
##  [99] 18.021957 23.136158
```
<br>
<strong>Step 3:</strong> Lets take the mean of the 'f' sample size.
<br>

```r
fbar <- mean(f)
fbar
```

```
## [1] 22.2608
```
<br>
<strong>Step 4:</strong> Lets apply the bootstrap principal to illustrate the centeral limit theorem. First we need to set the repetitions to 1000.
<br>

```r
nsims <- 1000
```
<br>
<strong>Step 5:</strong> Now we need to loop 1000 repetitions through the combined 'f' sample size of 100. In the loop the following occurs:
  
1. Pulls one value from the 'f' sample size
2. Puts the one value back into the orginal 'f' sample population
3. Calculates 1000 means
<br>
<br>

```r
bootnorm <- numeric(nsims)
 	for (i in 1:nsims) {
	temp <- sample(f, 100, replace=TRUE)
	bootnorm[i] <- mean(temp)
 	}
```
<br>
<strong>Step 6:</strong> Lets see the summary of the bootstrap simulation.
<br>

```r
summary(bootnorm)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   20.68   21.91   22.24   22.27   22.62   24.40
```
<br>
<strong>Step 7:</strong> Now we can compare the bootstrap mean to the orginal mean of the 'f' sample size. You notice how close they are of being equal to each other. Lets compare the standard deviations of the orginal 'f' sample and of the bootstrap data.
<br>
<br>
'f' Sample Standard Deviation<br>

```r
sd(f)
```

```
## [1] 5.396995
```
<br>
Bootnorm Sample Standard Deviation<br>
<br>

```r
sd(bootnorm)
```

```
## [1] 0.5326301
```
<br>
<strong>Step 8:</strong> If we take the standard deviation of the orginal 'f' samples size and divide it by the square root of the 'f' sample size off 100 the results should be the same as the orginal standard deviation of the 'f' sample. By comparing the two demostrates the central limit theorem.
<br>

```r
sd(f)/sqrt(100)
```

```
## [1] 0.5396995
```
