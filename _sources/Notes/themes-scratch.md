

Readings on stat/philosophy of science:
+ Statistical/modeling malpractice
    - Cargo-cult statistics
    - ASA $P$-values
    - https://www.nature.com/articles/s41599-020-00557-0
    - Saltelli et al. Manifesto https://www.nature.com/articles/d41586-020-01812-9
    - Gelman Loken Garden of Forking Paths
    - Benjamini selective inference
    - Pay no attention to the model behind the curtain
+ Interpretations of probability
    - Freedman Foundations of Statistics
    - LeCam note on metastatistics
    - Stark & Freedman What is the Chance of an Earthquake
+ Computational reproducibility
    - Donoho & Buckheit
    - Stodden on enhancing reproducibility https://science.sciencemag.org/content/354/6317/1240.summary
+ 
statistics
+ Random sampling: practice makes imperfect

Readings for applications
+ Macnell et al. / Boring et al.
+ Silberzahn et al.
+ Cicchetti declaration
+ Urban on extinctions
+ something on risk-limiting audits
+ Covid modeling: IHME / Jewell paper https://jamanetwork.com/journals/jama/fullarticle/2764824
+ Lockdowns and COVID spread https://onlinelibrary.wiley.com/doi/10.1111/eci.13484

Readings for methodology and numerical techniques
+ Benjamini & Hochberg
+ Fisher Lady Tasting Tea?
+ something on permutation tests
+ something on NPC
+ something on multiplicity
+ sequential tests and martingales


## Thread regarding computation
+ Version control: Git and GitHub 
+ Programming: Python
+ Process automation: Make
+ Data analysis: Numpy, Pandas, Matplotlib, NLTK, Scikit-Learn, …
+ Documentation: Sphinx and JupyterBook
+ Software testing: PyTest
+ Continuous Integration: Github Actions
+ Reproducible containers: Binder
+ Software design, modularity
+ Dependency management: environments & containers
+ Code review and public sharing & collaboration: licensing.
+ RNGs and numerical accuracy (chaos)
+ Literate programming and literate computing. nbdev

## Thread regarding epistemological questions & philosophy of science

+ Why? "Nullius in verba"
+ Evidence versus trust
+ Communication of uncertainty
+ What is probability?
+ Open science: sharing of code and data


## Thread regarding replicability

+ $P$-values
    - definitions, meaning
    - nominal versus actual $P$-values
    - the $P$-value controversy
    - does the statistical model match the science?
    - [aside: parametric versus nonparametric tests; permutation tests.](/V_nOKKssRISYIpy4gw8J9A)
    - Read: 
        + ASA collection on $P$-values
        + Freedman & Berk
        + MacNell et al.
        + Boring et al.
        + Silberzahn et al.
        + Cicchetti declaration
        + Random sampling: practice makes imperfect

+ combining $P$-values
    - why not just multiply tail probabilities?
        + Lottery fraud calculations
    - Fisher's combining function: independent case
    - other combining functions
    - nonparametric combination of tests
        + combining dependent $P$-values
    - multivariate tests from univariate tests
    - meta-analysis
    - Read:
        + Dream speedrun papers 
        + Boring et al.
        + Freedman & Berk
            
+ $P$-values and replication
    - Fisher on what it means to establish a scientific result
    - $r$-values
    
+ multiple testing
    - per-comparison error rate (PCER)
    - familywise error rate (FWER)
    - the false-discovery rate (FDR)
    
+ selective inference: "the silent killer"
    - illustrations
    - selection-adjusted tests
    - selective confidence intervals
        + error criteria FCR, SoS, SoP
    - Read:
        + Benjamini
        + Gelman and Loken