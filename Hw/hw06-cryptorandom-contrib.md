# Homework 6: Cryptorandom - contributing to an open source project

- **Statistics 159/259, Spring 2021**

- **Due 4/7/2021, 11:59PM PT**

- Profs. Pérez and Stark, Department of Statistics, UC Berkeley.

- This assignment is worth a maximum of **60 points**.

- Assignment type: **group**.


The purpose of this assignment is for your team to collaborate on the development of new contributions to a real-world open source repository, in this case the [`cryptorandom`](https://github.com/statlab/cryptorandom) project we've discussed in class.  The high-level goal of the assignment is to make contributions to `cryptorandom` in two areas: **testing** and **documentation**.

Think of this project as a scenario where your team are the maintainers of `cryptorandom`. You are starting from the code in its current state, and are going to work on the next release of the project. You will have to:

* Identify areas where you will make new contributions/fixes.
* Parcel out the work among team members.
* Review each other's work, that will be submitted to the team repository in the form of Pull Requests (PRs).
* Provide feedback and discussion for each PR.
* Ensure that each PR passes all existing tests and adds new ones as necessary. The project repo is already configured to run the test suite with Github Actions, but you will need to ensure that any changes you make are still covered by the automated execution.

While each team will work against a private fork of the official `cryptorandom` repo, we hope to later incorporate some of your contributions (with full public credit going to you) into the public repo. But your grade will _not_ be based on that - we only want you to be aware of this for you to know that we consider this a "real world" project.


## Grading

The entire assignment is worth 60 points, broken down as follows:

* 25 points: contributions to testing.
* 25 points: contributions to documentation.
* 10 points: release notes.

For each of the main areas (testing and documentation) we will look at the following aspects to assign points:

* Completeness and correctness of the issue addressed (new documentation or test). Each PR should be a meaningful contribution to the codebase, that is, it should actually improve the quality of the documentation or the coverage of the test suite, both in terms of line coverage and conceptual coverage.

* Open source workflow: 
  - Was a clear issue opened before starting work on the problem? 
  - Was the PR created with a clean set of commits that each address a separate part of the problem, and that contain descriptive commit messages?
  - Was the contribution correctly reviewed by team members, with appropriate feedback?
  - Did all members of the team participate in each aspect of the workflow? That is, creating issues, providing feedback, writing code, reviewing each other's PRs with meaningful feedback, etc?


## Workflow

* You will be assigned to a team of 4--5 students.
  - Each team will need to decide how to coordinate its work.
  - We will provide a private Slack channel for each team for "small" communication. You can call us for help there with the usual `@instructors` tag. 


* You *must* use Github issues as a "bulletin board" for each PR you will create. It's a good idea to create an issue describing the work you intend to do, and then create the PR that addresses it and closes it when merged. You can use [GitHub's automated linking of PRs, issues and commits](https://docs.github.com/en/github/managing-your-work-on-github/linking-a-pull-request-to-an-issue) to streamline this process.

* Your deliverable will consist of your team repository with a collection of merged or closed pull requests that implement all the requested functionality. 

* You will include at the top of the repository a file named `hw06-summary.md` that summarizes all your work, along with a PDF render of the same. This file should amount to _release notes_ that include:
  - a description of problems and gaps you found in the current docstrings
  - a description of problems and gaps you found in the main documentation
  - a description of problems and gaps you found in the unit tests
  - a description of each of your new tests and the functionality it tests
  - the coverage reports for your team's test PR.

* As an illustration of the kind of level of description and detail we have in mind, you can consult the [Numpy release notes](https://github.com/numpy/numpy/releases/tag/v1.20.0), but use your own judgment. You should think of this document as something that a third party interested in `cryptorandom` will be able to read to inform themselves about all the great new work that was done in this "new release."

* You will use a "pull cycle" development model. That is, no team member pushes directly to the team repository, but instead you each make your own personal fork of the team repo, and create pull requests into the team repo from your personal one.  This is how many real-world open source projects work (in fact, some enforce that no team member can push directly to the main repo even if they try).

* Each team member will create a separate branch for the development of each new feature/idea in their personal repository, and will make from there a PR to the team repo.

* Each team member _must_ make at least one PR related to documentation and one PR related to testing.
  - Each PR should be reviewed by _at least_ another student, with discussion and feedback provided in the PR.
  - Not all PRs need to be merged, but all need to be finalized: either merged, or closed with an appropriate discussion of why the team decided not to merge it.


## Tips for this assignment

_Note:_ some of these tips were previously in a separate document, now merged here as part of the homework (partly so the automated numbering scheme matches our homework numbers).

These notes should help you work through some of the issues we discussed in lecture, regarding how to render the sphinx documentation for `cryptorandom` in the hub, and how to then view your own build of these docs through the hub.

Basically we need to solve the following problems:

1. We need to ensure that pytest, Sphinx and other tools find and use our in-development version of `cryptorandom` instead of the system-wide one, so our new work is reflected in the tests and documentation we create.
1. We need to be able to build the documentation on JupyterHub and view the resulting docs online easily, through the Hub.

Credit and huge thanks to [Yuvi Panda](https://github.com/yuvipanda) from the JupyterHub/Berkeley team for his help navigating the proxy issues detailed below.


### Initial setup: personal and team repositories

You will need to fork the team repo to your personal user and then clone your personal fork into the hub. That will be your "working space", one for each member of the team. You will do all your work in your personal copy, pushing your changes up to github in your personal fork, and then from there, making PRs to the team repo. 

As we discussed in class, a good way to track both is to have _two_ remotes, using your personal fork as `origin` and the team repo as `upstream`. This also makes it convenient to have more remotes if for example you want to check locally the work of your teammate whose github username is `alice` by having a remote of that name.  As an illustration, this is what my remotes setup for the `cryptorandom` repo looks like on my system:

```
(base) (main)blanca[cryptorandom]> git remote -v
origin	git@github.com:fperez/cryptorandom.git (fetch)
origin	git@github.com:fperez/cryptorandom.git (push)
upstream	git@github.com:statlab/cryptorandom.git (fetch)
upstream	git@github.com:statlab/cryptorandom.git (push)
```


### Install `cryptorandom` locally in development mode

The first issue we must solve is for Sphinx to find the version of `cryptorandom` that you are working on, rather than the installed one. This manifests itself immediately as the `AttributeError` you see regarding a missing `__version__` attribute when trying to build the docs, but even if you fix that with a quick hack as I did in lecture, you'll still have a problem. The issue is that the docs will import the _system-wide installed_ version of `cryptorandom`, and not your local development copy. So any new docstrings or function signatures you edit will not be correctly reflected in the resulting docs.

The solution is to install your working copy as a _development version_, also known as an _"editable install"_ (hence the `-e` command line argument, short for `--editable`). We now explain how to do this, and you can find more details in the [pip documentation](https://pip.pypa.io/en/stable/reference/pip_install/#editable-installs).

In the top-level of the `cryptorandom` directory, where the file `setup.py` lives, run the command:

`pip install -e .`

You should see something like the following output (with your own user name in the path):


```
jovyan@jupyter-fernando-2eperez:~/cryptorandom> pip install -e .
Obtaining file:///home/jovyan/cryptorandom
Requirement already satisfied: numpy>=1.20 in /opt/conda/lib/python3.8/site-packages (from cryptorandom==0.3rc2.dev0) (1.20.1)
Requirement already satisfied: scipy>=1.6 in /opt/conda/lib/python3.8/site-packages (from cryptorandom==0.3rc2.dev0) (1.6.0)
Installing collected packages: cryptorandom
  Attempting uninstall: cryptorandom
    Found existing installation: cryptorandom 0.2
    Uninstalling cryptorandom-0.2:
      Successfully uninstalled cryptorandom-0.2
  Running setup.py develop for cryptorandom
Successfully installed cryptorandom
```

Check that you got it right by doing the following:

```
cd doc/
python -c "import cryptorandom as cr;print(cr.__version__)"
```

You should see:

```
jovyan@jupyter-fernando-2eperez:~/cryptorandom> cd doc/
jovyan@jupyter-fernando-2eperez:~/cryptorandom/doc> python -c "import cryptorandom as cr;print(cr.__version__)"
0.3rc2.dev0
```


### Set up the Sphinx build for JupyterHub-hosted viewing

Now we turn to the second problem: once we build our docs with Sphinx against our development version, how do we look at the built HTML results? These files are hosted in the Hub, not our home computer, so we can't easily view them immediately. While JupyterLab can display individual HTML files, this will not show a fully styled version with all the necessary extra assets such as images, CSS, etc.  We need to use a full _web server_ for that, and we need to be able to access that web server from outside the Hub. We now explain how to achieve this.

First, you need to make a change to `conf.py` so that the build can be seen through a JupyterHub installation. This change can probably go into cryptorandom proper in the end, but for now we suggest you make it directly into the team repo in a single commit, that all team members then pull from, so you all have it in one place. You need to add three lines below - the comment is there in the file already, around line 108, and we leave it here for ease of reference. You neeed to add the code starting with `import os`:

```python
# -- Options for HTML output ----------------------------------------------

import os

if "JUPYTERHUB_SERVICE_PREFIX" in os.environ:
    html_baseurl = f'{os.environ["JUPYTERHUB_SERVICE_PREFIX"]}/proxy/absolute/8000'
```

Just to make sure these changes apply everywhere, in the `doc/` directory run `make clean` once after the above, and then continue with the below. In what follows you may want to keep at least _two_ terminals open, one where you keep running the HTML Sphinx build, and one to run the server to check your builds (some might keep a third open in the top-level directory for git work, commits, pushes, etc). Take advantage of JupyterLab's ability to lay them out in whatever way you find most visually convenient!

Once you make these changes you should commit and push them to the team repo, and all members need to ensure they pull from that correctly and they all have the same `conf.py`.


### Editing the docs and testing your build

Make your edits and run `make html` in the `doc/` directory.  To check your build, then go to your other terminal (if you chose to have more than one) and go to the `build/html` subdirectory. There, run:

`python -m http.server`

as we saw today in class.  This will print a message like:

```
jovyan@jupyter-fernando-2eperez:~/cryptorandom/doc/build/html> python -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

but you can _not_ access `http://0.0.0.0:8000` as we explained today in class, as on your home computer that would correspond to a local port. Instead you need to reach that port but on the Stat159 DataHub!

In order to support that, the Hub runs what is called a proxy service, that basically hooks up port 8000 on the Hub service to a publicly available path on the internet, so that you can see that internal port from your home computer. 

The file you are trying to reach is `index.html` at the `doc/build/html` directory, being served on port 8000 on the server. To access that file from home, instead you tell your laptop to go to:

https://stat159.datahub.berkeley.edu/user-redirect/proxy/8000/index.html

(if you had configured the python HTTP server to use a different port than 8000 you'd change that number, and similarly if the name of the file you wanted to look at was different you'd adjust the path).

That URL will automatically change to a different one, with your username, and should show you the build of the docs. This is what that looks like for me when it's all running:

![](Fig/hw06-sphinx-build-hub-proxy-view.png)

As a side note, you may want to explore using [sphinx-autobuild](https://github.com/executablebooks/sphinx-autobuild), a tool that automatically builds and reloads your Sphinx docs as you make changes. I haven't personally tested it yet but it looks interesting, it is developed by the same team from the Executable Books project that builds JupyterBook.


### Development workfow

You can now keep the Python HTTP server running, and continue a cycle of making edits, running `make html` in the `doc/` directory, and checking the resulting HTML until it is to your liking.

Once you're happy, commit, push, make PRs, and communicate happily with your team on your progress!


### General suggestions on documentation

- check the docstrings within `cryptorandom.py` and `sample.py` and edit/augment them as you see fit.
- check whether the formal documentation accurately portrays the code.
- Read [this discussion about Four types of documentation](https://documentation.divio.com) for inspiration - you can make contributions in each of these dimensions. Docstrings aren't the only thing you can work on!
- To build the documentation you can type `make html` in the `doc/` subdirectory.


### General suggestions on testing

- Identify code that is not currently tested
- Identify tests that do not really "exercise" the code
- Make one PR that aims to push line-based test coverage as close to 100% as possible. This PR should also have individual tests that add *conceptual* test coverage in areas currently not covered.
- To run the test suite, you can run `make test-all` from the top-level directory, which is the same command that [the testing GitHub action uses](https://github.com/statlab/cryptorandom/actions/workflows/test.yml).
