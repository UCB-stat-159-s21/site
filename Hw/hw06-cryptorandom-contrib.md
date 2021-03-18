# Homework 6: Cryptorandom - contributing to an open source project

- **Statistics 159/259, Spring 2021**

- **Due 4/5/2021, 11:59PM PT**

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

## Suggestions

### Setup

You will need to fork the team repo to your personal user and then clone your personal fork into the hub. That will be your "working space", one for each person.

From your personal fork, you will need to install the working copy of cryptorandom so you can build the docs, run new tests, etc., against the version of the project you are actually writing code for. You can do this by running in your local copy the command

`pip install -e .`

as described in the `cryptorandom` README file.


### On documentation

- check the docstrings within `cryptorandom.py` and `sample.py` and edit/augment them as you see fit.
- check whether the formal documentation accurately portrays the code.
- Read [this discussion about Four types of documentation](https://documentation.divio.com) for inspiration - you can make contributions in each of these dimensions. Docstrings aren't the only thing you can work on!
- To build the documentation you can type `make html` in the `doc/` subdirectory.

### On testing

- Identify code that is not currently tested
- Identify tests that do not really "exercise" the code
- Make one PR that aims to push line-based test coverage as close to 100% as possible. This PR should also have individual tests that add *conceptual* test coverage in areas currently not covered.
- To run the test suite, you can run `make test-all` from the top-level directory, which is the same command that [the testing GitHub action uses](https://github.com/statlab/cryptorandom/actions/workflows/test.yml).


## Important temporary note

We need to make a few changes to the hub for this assignment, which are [currently under testing](https://github.com/berkeley-dsep-infra/datahub/pull/2252). Please check that link, if that PR isn't merged yet, then you'll need to run the following commands in a terminal in order to be able to successfully use the project:

```
pip install -U numpy==1.20.1
pip install numpydoc
```
