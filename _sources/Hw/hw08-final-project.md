# Homework 8. Final Project - Antibody Cocktail Efficacy

- **Statistics 159/259, Spring 2021**

- **Due Friday 5/14/2021, 11:59PM PT**

- Profs. Pérez and Stark, Department of Statistics, UC Berkeley.

- This assignment is worth a maximum of **100 points**.

- Assignment type: **group** (similar-sized teams as HW06).


The goal of this project is to implement and apply the method in section 3 of
[Li and Ding](https://onlinelibrary.wiley.com/doi/pdf/10.1002/sim.6764) for
confidence intervals, and apply it to the data from the [Regeneron
study](https://www.statnews.com/2021/04/12/regeneron-antibody-cocktail-covid-simple-injection/)
that claims their antibody cocktail is 81% effective at preventing symptomatic
COVID-19 infections in people living in a household with others who are already
infected, through 29 days after injection.


## [50 points] Code: confidence bounds

You will create a small python package called `cibin` that can be imported with
`import cibin` and tested at the command line with `pytest cibin`. This small
package will implement "Method 3" of Li and Ding in Python to find
2-sided $1-\alpha$ confidence bounds for the average treatment effect
in a randomized experiment with binary outcomes and two treatments (active treatment and control).

Note that both the Li and Ding paper, and the supplementary materials with an R
implementation, are available in the class Google Drive Literature Folder, for
you to use.  You should study the R code and paper as a reference and to run
validation tests, but you should create your own Pythonic implementation rather
than trying to translate R code line-by-line.

You can use cryptorandom and permute, along with your implementations of
hypergeometric confidence bounds from the previous homework assignment and any code we've provided from the class notebooks.

You must provide appropriate docstrings, unit tests, etc. Your code should comply with PEP-8 and PEP-257.

We have provided a [toy Python package on Github](https://github.com/fperez/mytoy) to show you how to structure a repository to contain a minimally installable Python package with the basics.  Feel free to copy the layout and basic `setup.py` file from that repo to get going.  You may also find the blog post series [Creating an open source Python project from scratch](https://jacobtomlinson.dev/series/creating-an-open-source-python-project-from-scratch/) valuable.

The deliverables for this part will be:

- The code in the `cibin` directory implementing these functions, with tests, docstrings, etc.

- A top-level notebook called `cibin-demo.ipynb` that reproduces, using your implementation, column "3" of table I in the Li and Ding paper.

The calling signature for the confidence procedure should be:

```python
tau_twosided_ci(n11, n10, n01, n00, alpha, exact=True, max_combinations=10**5, reps=10**3)
```

When `exact=True`, your function should compute the exact result (by enumerating all possible samples rather than using simulation), but it should stop by raising an exception if it hits the limit of `max_combinations`. This exception should indicate the required number of combinations so that you can increase the value of `max_combinations` to that value, if you are willing to pay that computational price.

You can for example see how scipy's [`newton_krylov`](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.newton_krylov.html) routine handles non-convergence for an illustration of this pattern that is common in scientific algorithms.

Conversely, when `exact=False`, then your code should perform `reps` number of total simulations per table tested to produce an approximate answer.

The function should return three two-element lists with the following information:

- `[lb, ub]`: lower/upper bound of the confidence interval.
- `[allocation that gives lb, allocation that gives ub]`. 
- `[# tables examined, total reps across simulations]`.

For this assignment, you may find the `combinations` function in the [Python itertools module](https://docs.python.org/3/library/itertools.html) useful. In general that module is a great resource for implementing (often tricky to get right) combinatorial algorithms, as it provides a number of well-tested basic building blocks.

Note that in the causal inference notebook there's an implementation (discussed during 4/29's lecture) of a few utility functions that can be handy for this work.  You are welcome to either look at them or use them verbatim, but we warn you **they have not been tested!**. Before you use them, you are responsible for testing and validating they are actually correct (and please let us know if you find bugs in them!).

## [20 points] Analysis Part I

Find 95% lower (one-sided) and two-sided confidence intervals for the reduction
in risk corresponding to the primary endpoint (data "Through day 29"), using
method 3 and also using the cruder conservative approach via simultaneous
Bonferroni confidence bounds for $N_{\cdot 1}$ and $N_{1\cdot}$ described in
the notes on causal inference. (For the Bonferroni approach to two-sided
intervals, use Sterne's method for the underlying hypergeometric confidence
intervals. Feel free to re-use your own code from the previous problem set.)

- Discuss the differences between the two sets of confidence intervals.

- Is it statistically legitimate to use one-sided confidence intervals? Why
  or why not?

- Are the 2-sided confidence intervals preferable to the one-sided intervals?
  Why or why not?


**Note:** for this and all parts below, write out your code and analysis narrative in one or more Notebooks or Markdown files at your discretion. You must name them `analysis-I`, `analysis-II`, etc. if you choose to break each part into its own file, or say `analysis-I-IV` if you combine multiple sections into one file.  Regardless of whether you use notebooks or markdown files, at the end you should compile them all to PDF and include them next to the source in the repo (tip: use a `Makefile`!).


## [10 points] Analysis Part II

Is the same method applicable to the two intermediate endpoints, symptoms
within 1 week and symptoms after 1 week? If so, how? Identify any additional
assumptions or adjustments that would be required to use the method on the
intermediate endpoints. If the method is not applicable to the intermediate
endpoints, explain why.

##  [10 points] Analysis Part III

Imagine enumerating all the subject-weeks (4 weeks per subject), and labeling
each as either "has symptoms" or "does not have symptoms," so that each week is
labeled with a binary outcome. Can either of the methods you implemented be
used to find confidence bounds for the average treatment effect, measured as
the reduction in the average number of symptomatic weeks per subject? If so,
explain how; if not, explain why.

##  [10 points] Analysis Part IV

Read the safety information and the information about the subjects in the press
release, including information about race, age, and risk factors. Based on the
evidence in the press release, would you recommend this prophylactic treatment
to a friend or relative? Why or why not? Is there something else you would want
to know first? If so, what?


## Author contribution statement

In the last one of your analysis files (depending on how you chose to split up your work), include an **Author Contribution Statement**, similar to what we requested in HW06 and HW07.

If you find yourself with an _important concern or disagreement_ regarding the team contribution statement that you feel requires private communication to the instructors, you can do so by [filling out this short form](https://forms.gle/v9iBZy4VTYYb3mbC9).


## Workflow

You will be assigned to similarly-sized teams from HW 6, and in some cases it may be the same people (we've done some reshuffling based on your feedback in HW 6 and 7, but didn't create a completely new set of teams from scratch). 

We will use the same workflow as for that assignment, with a private Slack channel for each team where we'll add the three instructors.  All other guidelines regarding testing, documentation, PRs, GitHub Actions and more, from the HW06 group assignment, apply equally here, so we won't repeat them. You can refresh your memory by [checking out those notes](hw06-cryptorandom-contrib.md#Tips-for-this-assignment).


## Resources

- [Example "toy" repository with a minimal, but full, Python package](https://github.com/fperez/mytoy).

- [Regeneron press release](https://www.statnews.com/2021/04/12/regeneron-antibody-cocktail-covid-simple-injection/).

- [Data tables for the above Press Release](https://investor.regeneron.com/news-releases/news-release-details/phase-3-prevention-trial-showed-81-reduced-risk-symptomatic-sars).

-  [Li and Ding (2016)](https://onlinelibrary.wiley.com/doi/abs/10.1002/sim.6764) and [supplementary materials](https://onlinelibrary.wiley.com/action/downloadSupplement?doi=10.1002%2Fsim.6764&file=sim6764-sup-0002-Supplementary.R)  (also in the Drive folder of literature).
