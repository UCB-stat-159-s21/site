# Homework 7: Permute - contributing to an open source project

- **Statistics 159/259, Spring 2021**

- **Due 4/25/2021, 11:59PM PT**

- Profs. Pérez and Stark, Department of Statistics, UC Berkeley.

- This assignment is worth a maximum of **40 points**.

- Assignment type: **group**.


The purpose of this assignment is for your team to collaborate on the development of new contributions to another real-world open source repository, the [`permute`](https://github.com/statlab/permute) project we've discussed in class.  The high-level goal of the assignment is to make contributions to `permute` in three areas: **functionality**, **tests** of that functionality, and **documentation** of that functionality.  All of the changes will be to the [`utils.py`](https://github.com/statlab/permute/blob/main/permute/utils.py) file.

The assignment involves improving and extending two existing functions: `binom_conf_interval` and `hypergeom_conf_interval`. Those functions compute 1-sided and 2-sided confidence intervals for the binomial parameter $p$ ($n$ known) and for the hypergeometric parameter $G$ ($N$ and $n$ known). The current implementations are variants of the "Clopper-Pearson" approach (see [Brown, Cai, and DasGupta (2001)](https://www.jstor.org/stable/2676784?seq=1)).

You will improve the two-sided intervals by adding a different method for the binomial and two different methods for the hypergeometric. The notes on [hypothesis tests](../Notes/tests.ipynb) and [confidence sets](../Notes/confidence-sets.ipynb) and code in those notes will probably be helpful.

Here are the goals of the assignment. They apply both to `binom_conf_interval` and to `hypergeom_conf_interval`.

## [15 points] 1-sided bounds

For both `binom_conf_interval` and `hypergeom_conf_interval`, test the 1-sided confidence bounds that are already implemented. Report on the following and provide code, tests and documentation as appropriate:

1. _[5 points]_ Check whether they correctly implement the mathematics. Correct them if not. 

1. _[5 points]_ Check the endpoints are found in a numerically stable and efficient manner. Provide a better method if not.

1. _[5 points]_ Add unit tests that exercise all the options.

## [30 points] 2-sided bounds. 

For both `binom_conf_interval` and `hypergeom_conf_interval`, test the 2-sided confidence bounds that are already implemented. Report on the following and provide code, tests and documentation as appropriate. (The $1-\alpha$ Clopper-Pearson two-sided confidence bounds are the intersection of a 1-sided upper $1-\alpha/2$ confidence interval and a 1-sided lower $1-\alpha/2$ confidence interval.)

1. _[5 points]_ Check whether the functions correctly implement the mathematics. Correct them if not.

1. _[5 points]_ Add unit tests that exercise all the options.

1. _[10 points]_ For both `binom_conf_interval` and `hypergeom_conf_interval`, extend the signature to include a `method` parameter. The default value of `method` should be "`clopper-pearson`". The `method` parameter should not affect how 1-sided confidence bounds are calculated.
    1. When `method="clopper-pearson"`, the 2-sided intervals should be calculated as the intersection of the 1-sided intervals using confidence level $1-\alpha/2$, based on the current implementation of the 1-sided bounds (or on your modification of the current implementation, if you improve them). This amounts to inverting 2-sided, significance level $\alpha$ hypothesis tests where the chance that the observation will be larger than the largest value in the acceptance region is not greater than $\alpha/2$ and the chance that the observation will be smaller than the smallest value in the acceptance region is not greater than $\alpha/2$. That is, it balances the probability of the tails.
    2. When `method="smallest-ar"`, the 2-sided intervals should be calculated by inverting tests that have the _smallest_ acceptance regions, following the approaches in the notes. Rather than balance the probability of the tails, this approach minimizes the number of outcomes in the acceptance region, which tends to produce shorter confidence intervals. To implement this method, consider writing helper functions that calculate the acceptance regions. That will make it easier to debug and test your work. **Note that there might be a bug in the implementation of 2-sided confidence bounds for binomial $p$ in the notes. Be sure you are implementing the right thing!**
    3. When `method="wang"`, the 2-sided intervals should be calculated using the "exact optimal" method of [Wang (2015)[( http://dx.doi.org/10.1080/01621459.2014.966191). (Note that the [supplementary materials](https://www.tandfonline.com/doi/suppl/10.1080/01621459.2014.966191) contain R code that purports to implement the method. We do not vouch for that code, but you might start by translating it into python.)
    4. If `method` takes any value other than "clopper-pearson", "smallest-ar", or "wang", the code should raise an exception.
    5. Provide unit tests for the new functionality and any helper functions.
    6. Provide appropriate docstrings for the new functionality.
    7. Follow PEP-8 and PEP-257.
    
1. _[10 points]_ Calculate (not simulate) the expected width of the 2-sided 95% confidence intervals for `method="clopper-pearson"` , `method="smallest-ar"`, and `method="wang"` for a range of values of
$n$ and $p$ (for the binomial) and for $N$, $G$, and $n$ (for the hypergeometric).
    1. This should be turned in separately as a Jupyter notebook (called `confidence-intervals.ipynb`).
    2. See the top of the left column of p.111 of [Brown, Cai, and DasGupta (2001)](https://www.jstor.org/stable/2676784?seq=1) for a hint of how to calculate the expected length of binomial confidence intervals. The expression for hypergeometric is analogous, but should use the hypergeometric pmf rather than the binomial pmf. 
    3. Discuss the difference between the two methods. 
    4. Which would you recommend, and why? If you would recommend one method over the other in some circumstances but not in others, explain why.


## Grading

The entire assignment is worth 40 points, broken down as follows:

* 15 points: work on 1-sided confidence bounds.
* 30 points: work on 2-sided confidence bounds.  Note that this includes as a deliverable, a standalone Jupyter notebook that you should add at the top of your team's repository, called `confidence-intervals.ipynb`.
* 5 points: summary release notes that highlight your changes to the various functions, called `hw07-summary.md`, along with a PDF render of the same.

As in the previous assignment, we will look at the workflow of opening issues and evolving your code as PRs on your repo.

## Workflow

You will be assigned to a small team of **2** students. We suggest that you use this as an opportunity to try out pair programming (here [some](https://martinfowler.com/articles/on-pair-programming.html) [resources](https://medium.com/@weblab_tech/pair-programming-guide-a76ca43ff389) you might find useful on this topic).

In this case, we will _not_ set up separate team Slack channels - you can talk to your partner via DM, and the two of you can ping `@instructors` if you need us for a private question, or ask on the `#homework` channel as usueal for anything that's not private (and we highly encourage public questions, as the answers may help everyone else as well).

Otherwise you should still work "in public" as before: Keep the team repo the system creates as your `upstream` and each of you make a personal fork that is your `origin`. Use Github issues as a "bulletin board" for each PR you will create, and do a proper code review of the PR on GitHub.   If you wrote the code together while pair programming you can note that fact in the PR review and keep it short, but you should still have a PR and some evidence of a public check on the work. This is part of the work of building public trust on an open source tool by communicating not only with one another, but also by leaving a public record for the rest of the community.

In general, all other guidelines regarding testing, documentation, PRs, GitHub Actions and more, from the HW06 group assignment, apply equally here, so we won't repeat them. You can refresh your memory by [checking out those notes](hw06-cryptorandom-contrib.md#Tips-for-this-assignment) as they apply equally to this one (obviously substituting the paths and names for the `permute` repo and project instead of `cryptorandom` as appropriate).