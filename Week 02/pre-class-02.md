# pre-class


Make sure you commit this often with meaningful messages. 

### Background

The exponential distribution is defined by its cumulative distribution function
\(F(x) = 1-e^{-\lambda x}\)

The R function ***rexp()*** generates random variables with an exponential distribution. For example 
<center><strong>rexp(n=10, rate=5)</strong> </center>

results in 10 exponentially distributed numbers with a rate \(\lambda=5\). If you leave out the 5 and just have
<center><strong>rexp(n=10) </strong></center>
then this results in 10 exponentially distributed numbers with a rate \(\lambda=1\), this is also referred to as the "standard exponential distribution". 

### Part 1


1. Generate 200 random values from the standard exponential distribution and store them in a vector `exp.draws.1`.  Find the mean and standard deviation of `exp.draws.1`.
    
    exp.draws.1<- rexp(n=200)
    mean.exp1<-mean(exp.draws.1)
    sd.exp1<-sd(exp.draws.1)


2. Repeat, but change the rate to 0.2, 5, 7.3 and 10, storing the results in vectors called  `exp.draws.0.2`,  `exp.draws.5`,  `exp.draws.7.3` and  `exp.draws.10`. 
    
    exp.draws.0.2<-rexp(n=200,rate=.2)
    mean.exp.2<-mean(exp.draws.0.2)
    sd.exp.2<-sd(exp.draws.0.2)
    
    exp.draws.5<-rexp(n=200,rate=5)
    mean.exp5<-mean(exp.draws.5)
    sd.exp5<-sd(exp.draws.5)

    exp.draws.7.3<-rexp(n=200,rate=7.3)
    mean.exp7.3<-mean(exp.draws.7.3)
    sd.exp7.3<-sd(exp.draws.7.3)

    exp.draws.10<- rexp(n=200,rate=10)
    mean.exp10<-mean(exp.draws.10)
    sd.exp10<-sd(exp.draws.10)


3. The function `plot()` is the generic function in R for the visual display of data. `hist()` is a function that takes in and bins data as a side effect. To use this function, we must first specify what we'd like to plot.
    a. Use the `hist()` function to produce a histogram of your standard exponential distribution. 
    
    hist(exp.draws.1)
    
    b. Use `plot()` with this vector to display the random values from your standard distribution in order.
   
    plot(sort(exp.draws.1),pch=20)
   
    c. Now, use `plot()` with two arguments -- any two of your other stored random value vectors -- to create a scatterplot of the two vectors against each other.
    
    plot(exp.draws.1,exp.draws.0.2,col=c("red","blue"),main="exp.draws.1 vs exp.draws.0.2" )

4. We'd now like to compare the properties of each of our vectors. Begin by creating a vector of the means of each of our five distributions in the order we created them and saving this to a variable name of your choice. Using this and other similar vectors, create the following scatterplots and explain in words what is going on:
    
    means<-c(mean.exp1,mean.exp.2,mean.exp5,mean.exp7.3,mean.exp10)
    
    rates<-c(1,.2,5,7.3,10)
    
    sds<-c(sd.exp1,sd.exp.2,sd.exp5,sd.exp7.3,sd.exp10)

    a. The five means versus the five rates used to generate the distribution.
    
    plot(means,rates,pch=20,main="Means vs Rates") 
   
    plot(rates,means,pch=20)
    
    The plot suggests that as the means increase, the rates decrease indicating a negative relationship between the two. 
    This negative relationship can be attributed to the nature of an exponential distribution where the rate is lamda, 
    and the mean is 1/lamda, therefore as the rate increases, the mean will decrease. Also, it is important to note that this     negative relationship is not linear, which is why we see a curved line that begins to straighten out as lamda increases
    and  1/lamda converges to 0. 
     
   
    b. The standard deviations versus the rates.
  
    plot(sds,rates,main="Sds vs Rates")
    
    plot(rates,sds)
    
    The plot suggests that the greater the standard deviation, 
    the lower the rate is. From 0 to 1, the effect the sd has on the rate is most
    significant, but the decrease in rate becomes less severe the greater the sd. In other words, the rate and 
    sd are inversely related, where the rate is lamda, and sd is 1/lamda, which is a property of the exponetial
    distribution and supported by the plots.
    
    c. The means versus the standard deviations.
    
    plot(means,sds,main="Means vs Sds")
    
    means.sds.lm<- lm(sds~ means)
    
    abline(means.sds.lm)

    The plot suggests that the means and standard deviations of each given distribution
    are equal.This makes sense because they are all exponential distributions, where the mean is 1/lamda,
    and the variance is 1/lambda^2. Taking the square root of the variance implies that both the sd 
    and mean are 1/lamda, hence we see a linear relationship between the two variables where y=x, or mean=sd.


For each plot, explain in words what's going on.

### Part II (PHP 2560 Only)


5. R's capacity for data and computation is large to what was available 10 years ago. 
    a. To show this, generate 1.1 million numbers from the standard exponential distribution and store them in a vector called `big.exp.draws.1`. Calculate the mean and standard deviation.
   
    big.exp.draws.1<- rexp(n=1100000)
    
    mean.big.exp1<-mean(big.exp.draws.1)
    
    sd.big.exp1<-sd(big.exp.draws.1)
    
    b. Plot a histogram of `big.exp.draws.1`.  Does it match the function \(1-e^{-x}\)?  Should it? 
    
    hist(big.exp.draws.1,main = " Question 5b")
   
    plot(1-exp(-x),pch=20)
    
    The histogram does not match the plot of 1-exp(-x) nor should it. The histogram is essentially the 
    pdf of an exponetial distribution, and 1-exp(-x) is the cdf of an exponential distribution. 

    
    c. Find the mean of all of the entries in `big.exp.draws.1` which are strictly greater than 1. You may need to first create a new vector to identify which elements satisfy this.
    
    WhichGreaterThan1<-which(big.exp.draws.1>1)
    
    ElementsGreaterThan1<-big.exp.draws.1[WhichGreaterThan1]
    
    mean(ElementsGreaterThan1)

    
    d. Create a matrix, `big.exp.draws.1.mat`, containing the the values in 
`big.exp.draws.1`, with 1100 rows and 1000 columns. Use this matrix as the input to the `hist()` function and save the result to a variable of your choice. What happens to your data?
    
   big.exp.draws.1.mat<-matrix(big.exp.draws.1,nrow=1100,ncol=1000)
    
   big.mat.hist<-hist(big.exp.draws.1.mat)
    
   Now the 1.1 million values are stored in a matrix with 1100 rows and 1000 columns, therefore there are still 1.1 million      values(ordered pairs/points). Plotting a histogram of this matrix is the same histogram as in part 5b. 

    e. Calculate the mean of the 371st column of `big.exp.draws.1.mat`.
   
   big.exp.draws.1.mat[,371]
   
   mean(big.exp.draws.1.mat[,371])

    f. Now, find the means of all 1000 columns of `big.exp.draws.1.mat` simultaneously. Plot the histogram of column means.  Explain why its shape does not match the histogram in problem 5b).
   
   ColMeans<-colMeans(big.exp.draws.1.mat)
   
   hist(ColMeans)
   
   The histogram resembles a normal distribution with mean at 1. The reason the histogram
   is approximately normal is because of the Central Limit Theorem, which applies because we are
   dealing with a distribution of means with large n, unlike in question 5b where we are dealing with individual                  observations from the expoenetial distribution that are not means.
