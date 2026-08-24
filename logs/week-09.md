# Week 9



## Goals
The paper was submitted at the start of this week. I took a rest after writing for days straight. Day, night and in dreams.
The goals have now shifted to produce deliverables and review experiment 

1. Answer weaknesses reviewer 2 would raise.
2. Position the work correctly in the generative information retrieval literature.
   


## Approach and Implementation
# Experiment Plan
1. Change one thing at a time.
Right now two parts of the identifier change together, so I cannot tell which one helped. Needed for: Methods, Discussion, Limitations.
2. Compare against older search methods.
The paper only compares my own versions to each other. It never compares them to a normal search system, which is the first thing a reviewer will ask about. Needed for: Related Work, Results, Discussion.
3.
Train more than once and test on more patients. Right now every number comes from a single run on a small number of patients. That is not enough to trust. Needed for: Dataset, Setup, Results, Limitations.
4. Count the errors instead of showing one.
The error section rests on a single example. I need to know how often each kind of failure happens. Needed for: Error Analysis, Discussion.
5. Write down the clustering settings.
They are not documented anywhere, so no one could repeat this work as written. Needed for: Methods, Setup.
Split the test set by whether age and sex are filled in. Compare the two groups.
6. This uses the models I already trained, so nothing has to be retrained. It tests the confound directly and is the cheapest thing on the list. Needed for: Results, Discussion.
7. Retrain using only trials that have age and sex filled in. Only worth doing if step 6 shows a real difference. Check how many trials are left before starting, since the completeness numbers suggest not many. Needed for: Results, Limitations.

## Results
The paper was submitted and I know what went wrong.
I need to do more experiments and get results and make final conclusions. The biggest mistake was making too many large changes at once.


## Notes
Write paper two weeks before deadline. Spend one week revising and getting feedback from advisor. 
Never wait last minute for a conference paper.

