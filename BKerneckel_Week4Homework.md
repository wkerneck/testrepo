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
##   [1] 23.004887 16.738799 17.274544 12.155595 22.334000 20.093512 25.410815
##   [8] 15.905875 22.069486 24.797592 23.822036 26.876708 20.582401 20.919067
##  [15] 30.437592 25.453516 22.373001 18.100196 22.663725 29.563650 23.646232
##  [22] 17.423505 20.632392 16.044565 25.480087 23.505537 11.205668 20.626260
##  [29] 21.241922 24.259148 18.534275 19.680835 24.625412 19.252048 21.338257
##  [36] 18.463423 19.424613 26.546921 29.143766 24.432395 19.109602 19.287236
##  [43] 26.608689 30.927255 23.059263 24.736394 31.909077  9.408133 12.050252
##  [50] 22.497290 27.198861 28.083579 16.431850 27.794627  5.509806 29.345025
##  [57] 28.218689 27.147116 21.618281 17.417529 23.661685 22.250093 22.176271
##  [64] 15.540606 25.752675 29.441009 22.628800 15.157732 30.454010 22.970302
##  [71] 30.353774 25.241627 25.108282 20.983279 30.468628 15.085874 26.350654
##  [78] 23.117663 21.682250 27.674718 13.986751 23.471966 16.458276 27.645376
##  [85] 21.491880 30.238843 23.068180 27.387192 18.638893 20.174682 29.611796
##  [92] 28.464866 22.675081 16.698789 18.108192 15.326026 25.865603 28.456852
##  [99] 25.215562 32.294603
```
<br>
  [1] 17.95230 25.39991 15.34891 27.45250 22.47374 21.63862 29.39335
  [8] 24.62867 23.54006 12.45266 16.78811 18.66860 10.11668 29.57409
  [15] 21.12169 25.03370 22.09456 24.38984 25.25218 27.04090 26.22417
  [22] 23.22323 17.78070 33.07141 20.16313 22.96748 21.82714 14.97591
  [29] 31.97083 25.03015 17.66355 18.12866 16.25695 22.04355 16.82819
  [36] 15.89339 27.62637 25.49004 19.71348 22.54881 22.56310 19.43644
  [43] 29.43888 23.70457 11.10911 27.32252 14.13592 23.61860 25.24690
  [50] 25.62334 25.97367 29.26052 21.12927 26.29818 17.90965 32.11575
  [57] 19.81381 24.37395 26.01842 28.49033 26.38283 25.35172 27.67909
  [64] 25.56680 28.62553 31.10062 20.66865 26.94472 24.51360 28.29204
  [71] 18.63688 24.42718 27.14154 27.53861 27.10827 29.58578 25.90789
  [78] 26.82669 25.99899 33.51179 22.66369 29.30563 27.05582 25.91018
  [85] 25.54653 22.48497 33.59645 30.44127 27.96189 26.87817 22.90093
  [92] 27.86020 30.89403 20.59696 24.90834 22.10812 20.38601 22.77556
  [99] 21.40030 21.23408
<br>
<strong>Step 3:</strong> Lets take the mean of the 'z' sample size.
<br>

```r
zbar <- mean(z)
zbar
```

```
## [1] 22.55822
```
<br>
 [1] 23.7134
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
##   20.80   22.19   22.59   22.57   22.93   24.75
```
<br>
    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   21.83   23.36   23.74   23.73   24.11   25.11
<br>
<strong>Step 7:</strong> Now we can compare the bootstrap mean to the orginal mean of the 'z' sample size. You notice how close they are of being equal to each other. Lets compare the standard deviations of the orginal 'z' sample and of the bootstrap data.
<br>
<br>
'z' Sample Standard Deviation<br>

```r
sd(z)
```

```
## [1] 5.330992
```
<br>
 [1] 5.394506
<br>
Bootnorm Sample Standard Deviation<br>
<br>

```r
sd(bootnorm)
```

```
## [1] 0.5496372
```
<br>
 [1] 0.5331759
<br>
<strong>Step 8:</strong> If we take the standard deviation of the orginal 'z' samples size and divide it by the square root of the 'z' sample size off 100 the results should be the same as the orginal standard deviation of the 'z' sample. By comparing the two demostrates the central limit theorem.
<br>

```r
sd(z)/sqrt(100)
```

```
## [1] 0.5330992
```
<br>
 [1] 0.5394506
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
##   [1] 24.021742 20.214402 21.338641 22.910210  9.303427 17.042386 19.512681
##   [8] 17.019822 23.092487 22.808749 19.471130 27.888881 25.507449 19.477910
##  [15] 18.200998 23.701456 18.545799 13.200985 19.147491 16.768657 28.262778
##  [22] 26.337461 23.531515 21.261322 18.261299 22.268736 15.979288 17.173363
##  [29] 25.023353 24.529590 26.106323 12.893406 20.203578 29.118115 18.694718
##  [36] 25.812063 17.951888 27.357071 22.905704 17.963424 23.366078 18.119486
##  [43] 23.151335 27.523236 21.607882 22.626393 19.791045 14.291233 18.999786
##  [50] 22.317421 20.976865 29.790211 25.819387 20.769624 15.979201 23.026327
##  [57] 26.881706 32.655723 29.847564 24.042162 29.461379 32.478477 21.404993
##  [64] 20.352879 17.381574 23.158821 33.224542 28.595102 17.619876 32.257139
##  [71] 28.198328 22.572847 24.772066 19.446802 25.587555 34.500106 15.981894
##  [78] 22.785762 17.802833 19.075622 33.588421 27.814590 17.887555 32.906762
##  [85] 22.571927 14.549423 23.719232 26.773779 34.369257 23.418109 18.400029
##  [92] 21.798315 26.937759 29.663086 29.255251 23.081891 29.425505 23.570630
##  [99] 22.053888 25.274889
```
<br>
[1] 19.37744 23.08717 16.03569 23.78391 23.99633 23.32191 15.17671
[8] 19.63743 18.06252 30.34188 24.49829 22.68173 15.68995 15.69673
[15] 24.05817 24.47685 22.16667 25.22224 25.37211 26.34389 23.48106
[22] 14.87901 23.50385 24.24096 26.68856 33.77304 17.28192 18.03052
[29] 14.70801 19.01180 18.18206 18.41709 20.02701 19.20585 18.60210
[36] 14.78920 11.99035 20.33790 21.32039 18.39136 28.51269 25.64741
[43] 20.77768 21.77162 23.08681 30.16801 27.59023 26.41070 19.12312
[50] 18.66324 21.95804 25.41038 25.77499 26.52709 20.70383 20.14878
[57] 18.20258 25.99257 26.84221 23.98272 24.60628 24.04886 30.64462
[64] 22.40420 26.76861 34.55708 19.67507 25.66844 29.85029 22.72216
[71] 28.45396 22.71466 34.68128 29.22041 27.19833 19.41800 30.13518
[78] 32.19048 12.82215 29.82833 22.75340 29.47965 33.57848 29.93012
[85] 30.10524 24.60930 14.32885 24.38899 27.08556 27.61868 25.27096
[92] 25.31993 30.95830 27.47501 27.58931 31.83941 17.08006 28.27521
[99] 32.11106 25.28377
<br>
<strong>Step 3:</strong> Lets take the mean of the 'f' sample size.
<br>

```r
fbar <- mean(f)
fbar
```

```
## [1] 22.96112
```
<br>
[1] 23.75874
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
##   21.14   22.60   22.97   22.97   23.31   24.50
```
<br>
    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   21.89   23.40   23.75   23.75   24.11   25.50
<br>
<strong>Step 7:</strong> Now we can compare the bootstrap mean to the orginal mean of the 'f' sample size. You notice how close they are of being equal to each other. Lets compare the standard deviations of the orginal 'f' sample and of the bootstrap data.
<br>
<br>
'f' Sample Standard Deviation<br>

```r
sd(f)
```

```
## [1] 5.22046
```
<br>
 [1] 5.220821
<br>
Bootnorm Sample Standard Deviation<br>
<br>

```r
sd(bootnorm)
```

```
## [1] 0.5211173
```
<br>
 [1] 0.5360274
<br>
<strong>Step 8:</strong> If we take the standard deviation of the orginal 'f' samples size and divide it by the square root of the 'f' sample size off 100 the results should be the same as the orginal standard deviation of the 'f' sample. By comparing the two demostrates the central limit theorem.
<br>

```r
sd(f)/sqrt(100)
```

```
## [1] 0.522046
```
<br>'
 [1] 0.5220821
