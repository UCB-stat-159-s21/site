# Homework 4: Reproducibility, Philosophy of Science, and COVID-19 Models

- **Statistics 159/259, Spring 2021**

- **Due 3/01/2021, 11:59PM PT**

- Profs. Pérez and Stark, Department of Statistics, UC Berkeley.

- This assignment is worth a maximum of **40 points**.

- Assignment type: **individual**.

The deliverables for this assignment are a markdown file, a .pdf rendering of the markdown file,
and a Jupyter notebook with text cells to annotate your work.

**Reading**

* Barba, L., 2018. Terminologies for Reproducible Research, https://arxiv.org/abs/1802.03311
* Buckheit, J.B., and D.L. Donoho, 1995. Wavelab and Reproducible Research, https://statweb.stanford.edu/~wavelab/Wavelab_850/wavelab.pdf
* Hakim, D. and E. Lipton, 2018.
Pesticide Studies Won E.P.A.'s Trust, Until Trump's Team Scorned 'Secret Science', _New York Times_,
24 August. https://www.nytimes.com/2018/08/24/business/epa-pesticides-studies-epidemiology.html
* Jewell, N.P.,  J.A. Lewnard,  and B.L. Jewell, 2020.
Predictive Mathematical Models of the COVID-19 Pandemic: Underlying Principles and Value of Projections,
_JAMA_, 323(19):1893-1894. doi:10.1001/jama.2020.6585
* Murray, C.J.L., and IHME COVID-19 health service utilization forecasting team, 2020. Forecasting COVID-19 impact on hospital bed-days, ICU-days, ventilator-days and deaths by US state in the next 4 months,
https://www.medrxiv.org/content/10.1101/2020.03.27.20043752v1.full-text
* Stark, P.B., 2018. Before reproducibility must come preproducibility, _Nature_, https://www.nature.com/articles/d41586-018-05256-0
* Stark, P.B., 2017. [Preface](https://www.practicereproducibleresearch.org/core-chapters/0-preface.html) to _The Practice of Reproducible Research_, J. Kitzes, D. Turek, and F. Deniz, eds., University of California Press, Berkeley
* Teytelman, L., 2018. No more excuses for non-reproducible methods, Nature, 560, 411. https://www.nature.com/articles/d41586-018-06008-w, doi: 10.1038/d41586-018-06008-w

## [20 points] Terminology and Philosophy of Science

+ [5 points] Explain in your own words different senses of the terms "reproducible," "replicable", 
and "repeatable."

+ [5 points] In your own words, explain why these concepts are important for science and for society.
    - What do reproducibility and replicability have to do with evidence?
    - Do you think there's a reasonable case for introducing a new term, such as "preproducible"
(not necessarily that word, but some new term)? Why or why not?
    - In your opinion, what role should scientific reproducibility and replicability play in public policy, for instance, in setting policy for mask-wearing or lockdowns?

+ [5 points] How could we solve the problem that different disciplines
use "reproducible," "replicable," and "repeatable" to mean different things?

+ [5 points] Comment on the new EPA rules prohibiting reliance on studies that are not sufficiently open.
    - Give some pros and cons.
    - What do you think the impact on public safety will be? Justify your answer.

There's no length requirement for this assignment, but we expect it to take
about 3-4 pages to do a good but concise job. 

**Deliverable:** Develop the answers to this part in a file called `terminology.md` and convert it to `terminology.pdf` (which you should include in your repository too) with `pandoc` at the terminal, as in previous assignments.


## [20 points] COVID modeling

+ [4 points] Explain the assumptions of the IHME COVID model described in Murray et al. (2020).
    - What are the parameters of the model? Explain the influence of each parameter on the cumulative number of deaths.
    - Can the model represent "waves" of infections? If so, how?
    
+ [4 points] List the five things you think make it hardest to predict COVID cases. 
    - Explain why you think they are the most serious difficulties.
    - Which, if any, are addressed in the IHME paper?
    - What do Jewell et al. (2020) have to say about those problems?

+ [12 points] Write a python function to fit the IHME model (the one in the first equation in the Murray et al. paper)
to a time series of COVID-19 deaths (not cases) using nonlinear 
least squares. You may use the
SciPy `optimize.curve_fit` function in your function. 
The function should return estimates of $\alpha$, $\beta$, and $p$.
You should include unit tests for your functions; your functions should be well documented; and you should run `pycodestyle` and `pep257` on your
code.
    - Use your function to fit the IHME model to the time series of deaths in Alameda County, California, as reported by Johns Hopkins University
here: https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_deaths_US.csv
The data are described here: https://github.com/CSSEGISandData/COVID-19/tree/master/csse_covid_19_data
        + Start with the first day on which the cumulative number of deaths was 4 or greater.
        + Fit the model to the first 30 days of data (starting with that day), the first 90 days of data, the first 180 days of data, and
the first 270 days of data, and all data through 2/15/2021.
        + Make a plot that superposes the data (through 2/15/2021) and the 5 fitted models, from the first day of data through 4/30/2021.
    - Comment on the reliability of the predictions


**Deliverable:** write a notebook called `covid-modeling.ipynb` with your written answers as well as the required code, figures and discussion.
