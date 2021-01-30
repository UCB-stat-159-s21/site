# Statistics 159/259, Homework 2. Election Fraud

- **Due 2/7/2021, 11:59PM PT**

- Profs. Perez and Stark, Department of Statistics, UC Berkeley

- This assignment is worth a maximum of **30 points**.


For this assignment, you will create a Jupyter Notebook called
`hw02-solution.ipynb` where you will type up your solutions. Create the
notebook with the contents of the questions below, and fill in your answer
below each question. You will need to add this new file to your repository and
push it back up to Github Classroom so we can see it. Please keep each top-level question (numbered heading with a [XX points] marker) _in a separate cell_.

**Problem context - claims of fraud in the 2020 US Elections:** Charles J.
Cicchetti, Ph.D., filed [a
declaration](https://www.supremecourt.gov/DocketPDF/22/22O155/163048/20201208132827887_TX-v-State-ExpedMot%202020-12-07%20FINAL.pdf
) in the recent Supreme Court challenge to the election results in several
states. Among other things, Cicchetti discusses hypothesis tests about the vote
in Georgia. Paragraph 11 reports a Z-score of 396.3; paragraph 12 reports a
Z-score of 108.7; and paragraph 15 reports a Z-score 1,891.

## [ 8 Points]  Explain the hypothesis tests. 

- What are the null hypotheses? 
- How is the Z-score calculated?
- How are the null hypotheses connected to election error or fraud in the 2020 election?
- Suppose the null hypotheses are false. Does that imply there was error or fraud in 2020?


## [ 6 Points] Find and retrieve the underlying election data and repeat his calculations. 

- Explain where and how you got the data and provide a reproducible way to find and retrieve them.
- Do you find the same inputs Cicchetti did? If not, explain.
- Do you get the same Z-scores reported in paragraphs 11, 12, and 15? If not, explain.
    
## [ 4 Points] Z tests

- What are the assumptions of a Z-test? What is the complete null hypothesis for a Z-test?
- Are the assumptions met here? Why or why not?


## [ 6 Points] Z tests in Cicchetti's analysis

Cicchetti's analysis assumes that votes are random and there is a given probability that
each voter will vote for the Democratic candidate, independent of all other voters. Suppose that's true.

+ What is the probability distribution of the number of votes for the Democratic candidate?
+ What is the probability distribution of the difference in vote shares across elections?
+ Do you think the normal approximation to that distribution is accurate to a part in a quintillion? Why or why not?

## [ 2 Points] What are the strengths of Cichetti's analysis?

## [ 2 Points] What are the shortcomings?

## [ 2 Points] How strong is Cicchetti's argument that the reported results in Georgia are wrong? Explain.


