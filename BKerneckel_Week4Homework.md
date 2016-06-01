# 2016-0509 MSDS 6304 Week 4 Homework
Bill Kerneckel  
May 27, 2016  
<br>
<br>
<strong><u>Assignment:</u></strong><br>

Write bootstrap code to illustrate the central limit theorem in R markdown and push the result to GitHub. Use a <strong>normal distribution</strong> with two different sample sizes and an <strong>exponential distribution</strong> with two different sample sizes. Please also comment on the code and explain the results. 

------------
####First Normal Distribution Sample Size
<br>
<strong>Step 1:</strong> Generate normal distribution with a sample size of 50, mean of 22, and a standard deviation of 5.
<br>

```r
x <- rnorm(50, 22, 5)
```
<br>
<strong>Step 2:</strong> Now lets output the combined 'x' sample size to see if our above statements worked.
<br>

```r
x
```

```
##  [1] 19.78445 20.40496 23.62111 24.41231 18.67561 26.03583 26.38897
##  [8] 22.55659 29.18691 19.43974 16.80642 17.23866 17.24799 28.49535
## [15] 24.14525 27.63908 20.31929 20.06453 22.05471 13.11043 26.40683
## [22] 23.54126 14.16110 30.18219 18.88095 26.53592 19.65323 26.00331
## [29] 22.11276 16.17189 11.77955 28.91943 17.24074 21.43422 16.61262
## [36] 19.25948 27.00411 15.60185 24.52970 20.28954 17.53021 26.43690
## [43] 20.56847 19.12113 17.88250 32.48089 24.71149 26.98447 25.21991
## [50] 22.18068
```
<br>
<strong>Step 3:</strong> Lets take the mean of the 'x' sample size and look at the distrubtion. We use this later to compare against the bootstrap principal.
<br>

```r
xbar.x <- mean(x)
xbar.x
```

```
## [1] 21.94131
```

```r
hist(x)
```

![](BKerneckel_Week4Homework_files/figure-html/unnamed-chunk-3-1.png)<!-- -->
<br>

<strong>Step 4:</strong> Lets apply the bootstrap principal to illustrate the centeral limit theorem. First we need to set the repetitions to 1000.
<br>

```r
nsims <- 1000
```
<br>
<strong>Step 5:</strong> Now we need to loop 1000 repetitions through the combined 'z' sample size of 50. In the loop the following occurs:
  
1. Pulls one value from the 'x' sample size
2. Puts the one value back into the orginal 'x' sample population
3. Calculates 1000 means
<br>
<br>

```r
bootnorm.x <- numeric(nsims)
 	for (i in 1:nsims) {
	temp <- sample (x, 50, replace=TRUE)
	bootnorm.x[i] <- mean(temp)
 	}
```
<br>
<strong>Step 6:</strong> Lets see the summary of the bootstrap simulation.
<br>

```r
summary(bootnorm.x)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   19.73   21.54   21.96   21.96   22.41   23.80
```

```r
hist(bootnorm.x)
```

![](BKerneckel_Week4Homework_files/figure-html/unnamed-chunk-6-1.png)<!-- -->
<br>

<strong>Step 7:</strong> Now we can compare the bootstrap mean to the orginal mean of the 'x' sample size. You notice how close they are of being equal to each other. Lets compare the standard deviations of the orginal 'x' sample and of the bootstrap data.
<br>
<br>
<table align=center width="600" border="0" cellpadding="5" cellspacing="5">
<tr>
<td width="300" align="center"><u>X Sample</u><td>
<td width="300" align="center"><u>Bootnorm X Sample</u></td>
</tr>
</table>
<table align=center width="600" border="0" cellpadding="5" cellspacing="5">
<tr>
<td width="300">
 Mean<br>

```r
mean(x)
```

```
## [1] 21.94131
```
<br>
Standard Deviation<br>

```r
sd(x)
```

```
## [1] 4.73764
```
</td>
<td width="300">
Mean<br>

```r
mean(bootnorm.x)
```

```
## [1] 21.95961
```
<br>
Standard Deviation<br>

```r
sd(bootnorm.x)
```

```
## [1] 0.6466144
```
</td>
</tr>
</table>

<br>

<br>

<strong>Step 8:</strong> If we take the standard deviation of the orginal 'x' sample size and divide it by the square root of the 'x' sample size of the orginal sample size (50) the results should be the near standard deviation of the x bootnorm sample. By comparing the two demostrates the central limit theorem.
<br>

```r
sd(x)/sqrt(50)
```

```
## [1] 0.6700035
```
<br>
<hr>
####Second Normal Distribution Sample Size
<br>
<strong>Step 1:</strong> Generate normal distribution with a sample size of 100, mean of 22, and a standard deviation of 5.
<br>

```r
y <- rnorm(100, 22, 5)
```
<br>
<strong>Step 2:</strong> Now lets output the combined 'y' sample size to see if our above statements worked.
<br>

```r
y
```

```
##   [1] 23.987540 18.529073 16.212310 17.300859 19.631855 20.662935 22.727420
##   [8] 25.600676 11.665007 19.907546 11.770537 16.191854 25.493218 20.247491
##  [15] 25.530519 32.088570 20.261035 18.298886 30.871645 22.675322 20.116176
##  [22] 21.629139 18.250878  9.804021 17.618904 27.304655 24.253423 26.013228
##  [29] 31.703692 24.875972 20.724488 29.550312 18.208046 34.544500 24.324525
##  [36] 22.405692 24.502371 22.321535 29.305870 22.360546 21.190794 25.166877
##  [43] 20.201715 22.168010 18.066031 20.292791 26.504386 14.465078 15.516684
##  [50] 12.735688 22.944504 12.970095 23.265786 16.036322 20.725314 23.927565
##  [57] 23.847930 32.186713 22.596266 25.743067 29.559431 25.725598 28.976959
##  [64] 24.168422 17.972599 28.723152 24.268243 24.574453 27.692959 17.970410
##  [71] 30.272767 21.751311 13.858486 17.301603 11.463956 11.126692 18.498136
##  [78] 14.814671 32.083465 21.790215 25.740792 19.108682 18.536413 23.584783
##  [85] 30.653836 21.211737 27.734610 34.651334 14.376873 13.005669 19.121832
##  [92] 21.426578 20.065357 24.290777 23.056645 30.288991 24.141710 26.613816
##  [99] 26.033298 16.958262
```
<br>
<strong>Step 3:</strong> Lets take the mean of the 'y' sample size and look at the distrubtion. We use this later to compare against the bootstrap principal.
<br>

```r
xbar.y <- mean(y)
xbar.y
```

```
## [1] 22.13219
```

```r
hist(y)
```

![](BKerneckel_Week4Homework_files/figure-html/unnamed-chunk-14-1.png)<!-- -->
<br>

<strong>Step 4:</strong> Lets apply the bootstrap principal to illustrate the centeral limit theorem. First we need to set the repetitions to 1000.
<br>

```r
nsims <- 1000
```
<br>
<strong>Step 5:</strong> Now we need to loop 1000 repetitions through the combined 'y' sample size of 100. In the loop the following occurs:
  
1. Pulls one value from the 'y' sample size
2. Puts the one value back into the orginal 'y' sample population
3. Calculates 1000 means
<br>
<br>

```r
bootnorm.y <- numeric(nsims)
 	for (i in 1:nsims) {
	temp <- sample (y, 100, replace=TRUE)
	bootnorm.y[i] <- mean(temp)
 	}
```
<br>
<strong>Step 6:</strong> Lets see the summary of the bootstrap simulation.
<br>

```r
summary(bootnorm.y)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   20.50   21.78   22.13   22.13   22.49   23.68
```

```r
hist(bootnorm.y)
```

![](BKerneckel_Week4Homework_files/figure-html/unnamed-chunk-17-1.png)<!-- -->
<br>

<strong>Step 7:</strong> Now we can compare the bootstrap mean to the orginal mean of the 'y' sample size. You notice how close they are of being equal to each other. Lets compare the standard deviations of the orginal 'y' sample and of the bootstrap data.
<br>
<br>
<table align=center width="600" border="0" cellpadding="5" cellspacing="5">
<tr>
<td width="300" align="center"><u>Y Sample</u><td>
<td width="300" align="center"><u>Bootnorm Y Sample</u></td>
</tr>
</table>
<table align=center width="600" border="0" cellpadding="5" cellspacing="5">
<tr>
<td width="300">
 Mean<br>

```r
mean(y)
```

```
## [1] 22.13219
```
<br>
Standard Deviation<br>

```r
sd(y)
```

```
## [1] 5.577694
```
</td>
<td width="300">
Mean<br>

```r
mean(bootnorm.y)
```

```
## [1] 22.12685
```
<br>
Standard Deviation<br>

```r
sd(bootnorm.y)
```

```
## [1] 0.5513176
```
</td>
</tr>
</table>

<br>
<strong>Step 8:</strong> If we take the standard deviation of the orginal 'y' sample size and divide it by the square root of the 'y' sample size of the orginal sample size (100) the results should be the near standard deviation of the bootnorm Y sample. By comparing the two demostrates the central limit theorem.
<br>

```r
sd(y)/sqrt(100)
```

```
## [1] 0.5577694
```
<br>

<hr>
<p>The next part of the home work assignment was to demostrate using a exponential distribution with two different sample sizes.</p>
<br>
<br>
####First Exponential Sample Size
<br>
<strong>Step 1:</strong> Generate exponential distribution with a sample size of 50.
<br>

```r
e <- rexp(50)
```
<br>
<strong>Step 2:</strong> Now lets output the combined 'e' sample size to see if our above statements worked.
<br>

```r
e
```

```
##  [1] 0.14705592 0.39257007 0.19310374 0.71802988 1.09292702 2.37931242
##  [7] 0.45316885 0.63629513 3.53403923 2.24302058 1.48728127 0.14304730
## [13] 1.28393986 0.04515311 4.21994486 0.03955300 1.20998072 1.36713668
## [19] 3.21256531 0.92999667 0.57843314 0.17452323 1.18987438 1.50277105
## [25] 1.88029364 1.50637994 0.10268337 0.18152795 0.75683065 0.34134527
## [31] 0.03333006 1.35441970 0.05117709 0.69846323 6.59838007 1.08371617
## [37] 0.33902147 0.79779888 0.16640675 1.92446718 0.36131038 0.13702715
## [43] 0.43563343 0.08003630 0.48204795 1.34381180 0.10241769 1.91838955
## [49] 0.33648929 0.42763728
```
<br>
<strong>Step 3:</strong> Lets take the mean of the 'e' sample size and look at the distrubtion. We use this later to compare against the bootstrap principal.
<br>

```r
xbar.e <- mean(e)
xbar.e
```

```
## [1] 1.052295
```

```r
hist(e)
```

![](BKerneckel_Week4Homework_files/figure-html/unnamed-chunk-25-1.png)<!-- -->
<br>

<strong>Step 4:</strong> Lets apply the bootstrap principal to illustrate the centeral limit theorem. First we need to set the repetitions to 1000.
<br>

```r
nsims <- 1000
```
<br>
<strong>Step 5:</strong> Now we need to loop 1000 repetitions through the 'e' sample size of 50. In the loop the following occurs:
  
1. Pulls one value from the 'e' sample size
2. Puts the one value back into the orginal 'e' sample population
3. Calculates 1000 means
<br>
<br>

```r
bootnorm.e <- numeric(nsims)
 	for (i in 1:nsims) {
	temp <- sample (e, 50, replace=TRUE)
	bootnorm.e[i] <- mean(temp)
 	}
```
<br>
<strong>Step 6:</strong> Lets see the summary of the bootstrap simulation.
<br>

```r
summary(bootnorm.e)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  0.5378  0.9171  1.0320  1.0460  1.1600  1.7550
```

```r
hist(bootnorm.e)
```

![](BKerneckel_Week4Homework_files/figure-html/unnamed-chunk-28-1.png)<!-- -->
<br>

<strong>Step 7:</strong> Now we can compare the bootstrap mean to the orginal mean of the 'e' sample size. You notice how close they are of being equal to each other. Lets compare the standard deviations of the orginal 'e' sample and of the bootstrap data.
<br>
<br>
<table align=center width="600" border="0" cellpadding="5" cellspacing="5">
<tr>
<td width="300" align="center"><u>E Sample</u><td>
<td width="300" align="center"><u>Bootnorm E Sample</u></td>
</tr>
</table>
<table align=center width="600" border="0" cellpadding="5" cellspacing="5">
<tr>
<td width="300">
 Mean<br>

```r
mean(e)
```

```
## [1] 1.052295
```
<br>
Standard Deviation<br>

```r
sd(e)
```

```
## [1] 1.237417
```
</td>
<td width="300">
Mean<br>

```r
mean(bootnorm.e)
```

```
## [1] 1.045646
```
<br>
Standard Deviation<br>

```r
sd(bootnorm.e)
```

```
## [1] 0.1772767
```
</td>
</tr>
</table>

<br>

<br>

<strong>Step 8:</strong> If we take the standard deviation of the orginal 'e' sample size and divide it by the square root of the 'e' sample size of the orginal sample size (50) the results should be the near standard deviation of the e bootnorm sample. By comparing the two demostrates the central limit theorem.
<br>

```r
sd(e)/sqrt(50)
```

```
## [1] 0.1749971
```
<br>
<hr>
####Second Exponential Sample Size
<br>

<strong>Step 1:</strong> Generate exponential distribution with a sample size of 100.
<br>

```r
f <- rexp(100)
```
<br>
<strong>Step 2:</strong> Now lets output the combined 'f' sample size to see if our above statements worked.
<br>

```r
f
```

```
##   [1] 1.972233541 0.235931922 0.346797765 0.300236464 0.646589227
##   [6] 3.530955391 0.264577499 4.106585037 0.585328583 0.511019531
##  [11] 1.729629822 2.001180043 0.205528114 0.896846064 0.622542863
##  [16] 0.340424220 0.458858151 2.417105773 0.570529007 1.001827053
##  [21] 0.686165245 2.555386899 0.937641947 1.281931284 1.257146103
##  [26] 1.654730512 1.122259395 0.662550497 0.120717346 2.621894252
##  [31] 0.243551966 0.989409170 1.709956515 0.577718896 0.228311911
##  [36] 0.133830674 2.740501458 0.961503266 2.274379844 1.175924410
##  [41] 0.366393783 2.944299526 0.389494225 0.009444345 0.366732331
##  [46] 3.535163115 0.087038031 2.503686311 1.787954297 1.011893686
##  [51] 2.050943909 2.039510574 3.639082512 0.753124576 2.919149863
##  [56] 0.651383539 0.252838837 2.016290530 0.108150874 0.740707454
##  [61] 1.014018440 0.226123209 0.022396308 2.955598093 0.535618484
##  [66] 2.518382059 2.076503092 0.772280432 0.404259659 0.945454789
##  [71] 0.268825716 0.645040719 3.758254176 0.695719553 1.029941155
##  [76] 0.397987165 0.417973016 1.442072352 0.710161176 0.997893529
##  [81] 0.347713243 1.420738060 0.750214767 0.772134177 6.021173908
##  [86] 1.664400954 0.459967162 0.397859529 0.188708582 0.273010512
##  [91] 0.159089382 0.356347951 0.205142439 0.192517592 0.242226246
##  [96] 0.463688763 0.355818183 2.774231367 7.407243710 0.254628321
```
<br>
<strong>Step 3:</strong> Lets take the mean of the 'f' sample size and look at the distrubtion. We use this later to compare against the bootstrap principal.
<br>

```r
xbar.f <- mean(f)
xbar.f
```

```
## [1] 1.213949
```

```r
hist(f)
```

![](BKerneckel_Week4Homework_files/figure-html/unnamed-chunk-36-1.png)<!-- -->
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
bootnorm.f <- numeric(nsims)
 	for (i in 1:nsims) {
	temp <- sample (f, 100, replace=TRUE)
	bootnorm.f[i] <- mean(temp)
 	}
```
<br>
<strong>Step 6:</strong> Lets see the summary of the bootstrap simulation.
<br>

```r
summary(bootnorm.f)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##  0.8267  1.1190  1.2040  1.2080  1.2860  1.6680
```

```r
hist(bootnorm.f)
```

![](BKerneckel_Week4Homework_files/figure-html/unnamed-chunk-39-1.png)<!-- -->
<br>

<strong>Step 7:</strong> Now we can compare the bootstrap mean to the orginal mean of the 'f' sample size. You notice how close they are of being equal to each other. Lets compare the standard deviations of the orginal 'f' sample and of the bootstrap data.
<br>
<br>
<table align=center width="600" border="0" cellpadding="5" cellspacing="5">
<tr>
<td width="300" align="center"><u>F Sample</u><td>
<td width="300" align="center"><u>Bootnorm F Sample</u></td>
</tr>
</table>
<table align=center width="600" border="0" cellpadding="5" cellspacing="5">
<tr>
<td width="300">
 Mean<br>

```r
mean(f)
```

```
## [1] 1.213949
```
<br>
Standard Deviation<br>

```r
sd(f)
```

```
## [1] 1.275904
```
</td>
<td width="300">
Mean<br>

```r
mean(bootnorm.f)
```

```
## [1] 1.208028
```
<br>
Standard Deviation<br>

```r
sd(bootnorm.f)
```

```
## [1] 0.1275414
```
</td>
</tr>
</table>

<br>
<strong>Step 8:</strong> If we take the standard deviation of the orginal 'f' sample size and divide it by the square root of the 'f' sample size of the orginal sample size (100) the results should be the near standard deviation of the bootnorm F sample. By comparing the two demostrates the central limit theorem.
<br>

```r
sd(f)/sqrt(100)
```

```
## [1] 0.1275904
```
