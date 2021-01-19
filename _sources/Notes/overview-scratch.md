## Topics 

### Computational hygiene and best practices (python-centric)
- style standards
    - coding [PEP-8](https://www.python.org/dev/peps/pep-0008/)
    - docstrings [PEP-257](https://www.python.org/dev/peps/pep-0257/)
- ["literate" programming](http://www.literateprogramming.com/): code for clarity. "Documentation containing code, not code containing documentation" 
- modularity, abstraction, function signatures
- revision control systems
    - Git fundamentals
    - Git as an intelligent backup tool
    - Git as a collaboration tool
    - Git development workflows
- testing
    - unit tests
    - regression tests
    - coverage tests
    - continuous integration; Github actions
- code performance, profiling

### Reproducibility, replicability, applied statistics

+ What is reproducibility?
    - Why is reproducibility an issue?
    - Terms in different fields: computational, experimental, ...
    - "Preproducibility"
    - What is contributing to lack of reproducibility in science?
    - Importance of replication in the philosophy of science
    - "Virtual witnessing"

+ Attempting computational reproducibility in data analysis
    - data
        + get the data
            - can be hard even if journal/funder requires making data available
        + figure out what format it's really in
            - data dictionaries sometimes help
            - proprietary formats common
        + figure out whether it's the right data
            - sniff tests
            - consistency tests
            - sleuthing
        + pre-processing, cleaning, etc.
    - analysis
        + figure out what they claim to have done
        + figure out what they did 
            - usually impossible from just the methods section
            - much harder if the analysis was not scripted
            - might be impossible even with their code
        + figure out what they should have done
        + compare

+ Sciencing is hard
    - confirmation bias
    - easiest person to fool is yourself. "The core of [the scientific method] is remembering your own level of ignorance." —Jaron Lanier
    - misperceptions of probability, cognitive biases (see seminal research by Tversky and Kahneman)
    - confidence and accuracy unrelated
    - shiny models and methods often distract rather than illuminate
    - broken reward structure
    - ritualization
    - Cargo-cult science and statistics

+ Papers/Datasets for the term
    - papers where there seemed to be a chance to get the data
    - topics with social impact: politics, health, ...
    - some papers we think are bogus
    - some papers whose conclusions we like--inviting scrutiny to combat our own confirmation bias

+ Software engineering
    - revision/version control
    - documentation
    - modularity and abstraction
        - consistency: APIs, calling signatures, object-oriented coding
        - separating data, computation, presentation
        - how general is the problem your approach can solve?
            - what's the right level of abstraction?
            - does it solving it require other broadly useful tools?
            - consider other approaches to subproblems? 
            - don't re-invent the wheel...but understand how wheels work
    - unit tests, integration tests, regression tests, coverage tests
    - code review
    - pair programming
    - scripted analyses
    - automation
    - accountability

+ Case study: Karp et al., 2015
    + access to data
    + reproducing the main results from the data
    + regression models
        - assumptions required to perform OLS
        - assumptions required for OLS to be unbiased
        - assumptions required to compute SE
        - assumptions required for $\hat{\beta}/SE$ to have a t-distribution
    + interpreting P-values
        - what's the null hypothesis?
        - appropriateness of t-tests in regression
        - p-values from observational data: hypothetical randomness
    + permutation tests
        - group invariances and exchangeability
        - the Neyman "ticket" model
            + the strong null hypothesis and weak null hypotheses
        - interference
            + when is non-interference a reasonable assumption?
        - null hypotheses, tests, and test statistics
            + key restrictions
            + significance versus power
            + specific alternatives and omnibus alternatives
            + p-values versus fixed-level tests
        - generating random permutations. See [Stark 2017](https://www.stat.berkeley.edu/~stark/Seminars/prngCDAR17.slides.html)
            + generating pseudo-random numbers and pseudo-random integers
            + LCGs, Mersenne Twister, cryptographic PRNGs
            + shuffling algorithms
            + the [cryptorandom library](https://github.com/statlab/cryptorandom/tree/master/cryptorandom)
            + problems with R's algorithms for generating random integers and random samples [Ottoboni & Stark](https://arxiv.org/abs/1809.06520)
        - confidence bounds for p-values by inverting binomial tests See [Permute/utils binom_conf_interval](https://github.com/statlab/permute/blob/master/permute/utils.py)
    + from reproducibility to replicability, stability, and generalizability
        - transforming data before regression: "Garden of forking paths." See [Gelman & Loken](http://www.stat.columbia.edu/~gelman/research/unpublished/p_hacking.pdf)
        - sensitivity of conclusions to transformations
        - sensitivity of conclusions to individual data: "influential observations"
        - testing before modeling and post-selection inference (POSI)
        - why reporting everything you tried matters; pre-registration
            + [AllTrials.net](http://www.alltrials.net)
            + changing clinical endpoints. Example: [PACE trial for CFS/ME](http://www.virology.ws/wp-content/uploads/2016/09/preliminary-analysis.pdf)
        
+ [Statistical models and response schedules](https://github.com/pbstark/S157F17/blob/master/models.ipynb)
    - Response schedules and "physics." See [Freedman SMTP Ch6](./Lit/freedman09-SMTP-response-schedules.pdf)
    - Linear probability models
    - Logit and probit models 
    - Poisson regression
    
+ [Goodness of fit tests](./Code/goodness_of_fit.ipynb)

+ [Bayesian and frequentist estimation and inference](./Code/bayes.ipynb)
    - Foundational issues
    - Interpretation of probability
        + prior probabilities 
    - Example problems
        + Bounded normal mean
        + Election auditing
    - Abstract framework
    - Types of uncertainty
        + Epistemic and aleatory uncertainty
        + constraints versus priors
    - Bayesian and frequentist measures of uncertainty
    - Duality between minimax and Bayes estimation
    
+ Example: [Election audits](https://github.com/pbstark/S157F17/blob/master/audit.ipynb)
    - The auditing challenge and [evidence-based elections](https://www.stat.berkeley.edu/~stark/Preprints/lhc18.pdf)
    - [Public evidence from secret ballots](https://arxiv.org/pdf/1707.08619.pdf)
    - Sequential tests
        + [Wald's SPRT for Binomial $p$](https://github.com/pbstark/S157F17/blob/master/sprt.ipynb)
        + [Wald's SPRT for dependent observations](https://github.com/pbstark/S157F17/blob/master/pSPRTnoReplacement.ipynb)
    - Transparency, reproducibility, auditability, and evidence in elections
        + public observation, public notice
            - observation versus evidence
        + data disclosure, "commitments"
        + [selecting the seed as a public ritual](https://youtu.be/ysG4pFFmQ-E?t=960)
        + source disclosure
            - PRNG
            - mapping from PRNG to sample
            - risk calculations 
            - escalation rule and (most importantly) stopping rule
        + procedural complexity
            - what can a single observer observe?
            - what does the public have to trust to have trust in election outcomes?
        + examples of disclosed tools
            - [tools for ballot-level comparison audits](https://www.stat.berkeley.edu/~stark/Vote/auditTools.htm)
            - [tools for ballot-polling audits](https://www.stat.berkeley.edu/~stark/Vote/ballotPollTools.htm)
            - [SUITE](https://github.com/pbstark/CORLA18)
            - [RLATool](https://github.com/FreeAndFair/ColoradoRLA) [new version](https://github.com/democracyworks/ColoradoRLA)
    - Contrasting RLAs and Bayesian audits
        + what question does the audit answer?
            - this election, or a hypothetical population of elections generated from known distribution?
        + whence the prior?
        + when are Bayesian audits RLAs?

+ [Stratified tests and Fisher's Combining Function](https://github.com/pbstark/S157F17/blob/master/combining-tests.ipynb)
    - why stratify or combine tests?
    - intersection-union tests and union-intersection tests
    - combining functions
    - combinations of independent $p$-values
        + chi-square distribution for continuous $p$-values (under the null)
        + stochastic dominance by chi-square when the distribution has atoms
        + dependent tests and lockstep permutations
    - nuisance parameters
    - [SUITE](https://github.com/pbstark/CORLA18)
 

## Best uses for Jupyter notebooks

+ Jupyter notebooks are a wonderful tool for exploratory data analysis, to present results
and to provide a "narrative" analysis: quantitative storytelling, showing the steps of the
analysis and explaining the underlying mathematics, science, etc.

+ Jupyter notebooks are not an ideal tool to develop a codebase for a project, to house production tools, 
etc. Jupyter isn't suited to automated testing or continuous integration 
(there's no tool for that in Jupyter, as far as I know). A software development project is generally
easier to build and maintain if you separate tests from the code, in different files.

+ Jupyter isn't suitable for packaging/distributing code or for providing tools 
to be imported into other analyses. For those purposes, you want python files.

+ Once you have built the software tools (and tests of those tools) you need for an analysis 
project, running analyses using 
those tools in a well documented Jupyter notebook that tells the story of what you did so 
that others can reproduce it is a good use of the overall tool ecosystem.