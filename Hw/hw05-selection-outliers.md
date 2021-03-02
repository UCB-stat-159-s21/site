# Homework 5: Selective inference and outlier rejection

* **Statistics 159/259, Spring 2021**
* **Due 3/8/2021, 11:59PM PT**
* Profs. Pérez and Stark, Department of Statistics, UC Berkeley.
* This assignment is worth a maximum of **40 points**.
* Assignment type: **individual**.

This brief assignment (a little computation and a modest amount of thinking) uses simulation to illustrate
the problem of selective inference (selecting what to compute or report based on the the data) 
and why blind "rejection" of outliers can be misleading.

Both topics have to do with "researcher degrees of freedom," i.e., decisions the data analyst
makes that can alter or distort the results and conclusions.
See, e.g., [Gelman, A., and E. Loken, 2014. The Statistical Crisis in Science, _American Scientist_,
102, 460--465](http://stat.columbia.edu/~gelman/research/published/ForkingPaths.pdf).

**Deliverable:** for this assignment, please turn in:

- One notebook that includes code for plots and simulations, along with your written responses and discussion. Please remember to use markdown headings for each section/subsection so the entire document is readable.

- The notebook should include the capture of the run of your unit tests like you've done before (see next point).

- A python file called `lognormals.py` with your three implementations of a lognormal random variable, accompanied by a file called `test_lognormals.py` that includes the unit tests. 


## [20 points] Selective inference

Imagine that you are selecting variables to include in a regression model. 
A common method for selecting which coefficients/variables/parameters to include in a 
regression or other statistical model is to keep the variable if the estimated coefficient 
$|\hat{\theta}|$ is "significant," i.e., if the t-statistic or z-statistic for the estimated 
coefficient is large.  
Having chosen which variables to keep using a method like that, analysts often then report 
confidence intervals for the coefficients, as if they had not already used the data to 
decide which variables to keep in the model. 
This is called "selective inference," as described in the citations below. 
Selective inference leads to problems with statistical reproducibility for many reasons. 
This assignment highlights one of them: confidence intervals can be far less likely to 
contain the true value of the parameter when you use the data to select which parameters to 
report confidence intervals for.

To keep things simple, we will pretend that the standard error of the coefficient is known
(and is equal to one), rather than estimated, so instead of using Student's $t$ distribution 
we can use the standard normal distribution. 
In this exercise, $X$ plays the role of $\hat{\theta}$.
You will simulate $X \sim N(\theta, 1)$; $X$ is then an unbiased estimate of $\theta$.

[3 points]

+ For each $\theta \in \{-3, -2.9, \ldots, -0.1, 0, 0.1, \ldots, 2.9, 3 \}$, simulate a
draw $X \sim N(\theta, 1)$.

+ If the draw is "statistically significant at level 0.05," i.e., if $|X| \ge 1.96$,
construct the usual 95% confidence interval for $\theta$ from the draw, i.e., $[X-1.96, X+1.96]$.
If $|X| < 1.96$, do not make a confidence interval.
For each confidence interval, record whether it contains the value of $\theta$ used to generate $X$.
Repeat until you have constructed 10,000 confidence intervals for each value of $\theta$.

[3 points]

+ Plot the fraction of the 10,000 confidence intervals for $\theta$ that contain $\theta$, 
as a function of $\theta$.
(I.e., plot the empirical coverage rate of the confidence intervals.)

[3 points]

+ Include unit tests for every function.

[3 points]

+ Explain why the plot looks the way it does.

[8 points]
+ Suppose you wanted to create a procedure that had at least 95% coverage probability, no
matter what $\theta$ is. 
    - Sketch how you would have to modify the usual normal confidence interval.
(I don't expect you to work out the math, just explain heuristically how the confidence interval
would have to behave.) 
    - Would the interval be symmetric around $X$? 
    - Would it be longer or shorter than the standard interval? 
    - What other differences would you expect?


_Hint:_ consider asymmetric confidence intervals.

_Extra hint:_ see

* [Benjamini, Y. and D. Yekutieli, 2005. 
False Discovery Rate-Adjusted Multiple Confidence Intervals for Selected Parameters, 
_Journal of the American Statistical Association, Theory
and Methods_, _100_(469), DOI 10.1198/016214504000001907](https://www.tandfonline.com/doi/abs/10.1198/016214504000001907) 
* The [online Seminar on Selective Inference](https://www.selectiveinferenceseminar.com) is a great resource on this topic. In particular you may want to watch the talk on "Confidence Intervals for Selected Parameters" by Benjamini - [recording](https://drive.google.com/file/d/1D2cq1n_e0LlbxvQjyG0feNKPd4GY1ZCe/view?usp=sharing), [slides](https://drive.google.com/file/d/1qGk4wFZkBEizYEUyGL7HCaduV_GXNMvj/view) and [preprint co-authored with Hechtlinger & Stark](https://arxiv.org/abs/1906.00505).

## [6 points] Outlier rejection and the trimmed mean

It is common to discard extreme data as "outliers." 
Two common ways of dealing with putative outliers are to discard observations that are
more than some number of sample standard deviations from the sample mean ("outlier rejection") and to discard
some fraction of the most extreme observations (the "trimmed mean" and related statistics).
This exercise explores the effect discarding extreme observations
can have on the bias, accuracy, and reliability of estimates.

[Uttl and Violo (2020)](https://www.scienceopen.com/document?vid=b1353421-2e05-4a79-9c6f-4ac5a44dcc03) 
claim that the conclusions of MacNell et al. (2015) are incorrect because MacNell et al. include
three outliers. 

[1 point]
+ What are Uttl and Viola's arguments to justify discarding data?

[1 point]
+ What are the assumptions of their arguments?

[2 points]
+ Sketch a real-world scenario where you think it is scientifically justified to discard "outliers," 
and explain why it is justified.

[2 points]
+ Sketch a real-world scenario where you think it is not scientifically justified to discard "outliers,"
and explain why.

## [14 points] Outliers: computational example

This example involves simulating from a lognormal distribution. It shows that discarding extreme
observations can produce misleading results, both for point estimates and confidence intervals.

### [6 points] Implementation Comparison

Implement three separate ways of simulating a lognormal random variable:

  - use `scipy.stats.lognorm`
  - use `scipy.stats.norm` and exponentiate
  - use `scipy.stats.uniform` and the inverse probability transformation (you can use the scipy implementation of the normal CDF and inverse normal CDF as part of your solution)

Notes:

- the calling signatures and return signatures of the three functions should be the same
- provide comparisons and appropriate unit tests for the latter two approaches. Run a timing comparison (remember the `%timeit` magic), and think of how you can validate that all implementations are ultimately giving the same answer.
- explain why the inverse probability transform method for simulating random variables involves the assumption that the distribution is continuous. 
  + What goes wrong (or has to be changed) if the distribution is discrete? 
  + If you can, provide a more general approach that also works for discrete random variables and for random
variables that are "mixed" (neither continuous nor discrete)
+ What is the expected value of a lognormal distribution with parameters $\mu=0$, $\sigma=1$?

### [4 points] Trimmed mean
+ Repeat 10,000 times:
    - simulate 40 draws from a standard lognormal distribution
    - calculate the 5% trimmed mean (i.e., discard the 5% smallest and 5% largest observations--two points
from each end--and take the mean of the remaining 36 points)
    - calculate a "formal" normal 95% confidence interval based on the 36 remaining points, that is,
the trimmed mean plus and minus 1.96 times the sample standard deviation of the 36 points, divided by 6,
(the square root of 36).
+ compare the mean of the 10,000 trimmed means to the true expected value of the lognormal distribution, and report the
percentage of the 10,000 intervals that contain the true expected value. 
    - Explain why the mean of the sample means differs from the expected value of the lognormal in the direction it does.
    - Explain why the percentage of intervals that cover the true expected value differs from 95% in the direction it does.

### [4 points] Outlier rejection
+ Repeat 10,000 times:
    - simulate 40 draws from a standard lognormal distribution
    - discard any observations that are more than 2 sample standard deviations from the sample 
mean. Take the mean of the remaining points.
    - calculate a "formal" normal 95% confidence interval based on the remaining points, that is,
the mean plus and minus 1.96 times the sample standard deviation of the remaining points, divided by the square
root of the number of remaining points.
+ compare the mean of the 10,000 "outlier-rejection" means to the true expected value of the lognormal distribution, and report the
percentage of the 10,000 intervals that contain the true expected value. 
    - Explain why the mean of the sample means differs from the expected value of the lognormal in the direction it does.
    - Explain why the percentage of intervals that cover the true expected value differs from 95% in the direction it does.
    