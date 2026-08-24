---
layout: post
title: "Week 7: New direction"
---
# Week 7

**Dates:** 06-22 to 06-28

## Goals
We are back to working on the trainer. Basic Seq-To-Seq T5. Train. Look at results. Change into a new direction and retrain. Review results, rinse and repeat. I am getting used to having poor results, but I am glad to have results. 
1. No Synthetics Patients, Using TREC 2021 Trials patients. That problem is done.
2. Fixed T5 on GPU. I had that issue fixed with a small test, so training will take 15 minutes.
3. The DocID is from Cluster from PubMedBert, Specialty, Age Band, Gender/Sex/Health Volunteer, and NCT Trial to fulfill unique DocID requirement.
4. Write script that double-checks for no collisions, all new identifiers are unique and hallucination-proof. 
   

## Approach and Implementation
Three things to work on, the data, the training model and the DocID. Conversion to the semantic DocID was easily. I just use converter script that assigned the the clusters to the trial docs from the TriaLGPT files, then created a new version of the documents with the semantic ids. The old version used the arbitrary DocIDs (001, 002,..., .etc), mine use (Cluster-Specialty Bit Mask- Age - Sex- NCT Tail ). A small change, and something I can feel confident as my own contribution. 

The synthetic patient dataset I generated was used only as placeholder and helped set up earlier data verification and printing of how I wanted the output to look like. Now that this I need it for this session's work, I've looked into what TREC 2021 patient topics are formatted and did the necessary replacement with little touch up. 

Additionally, I ran a hierarchical k-means over the embeddings to produce the cluster field. No more memorizing strings, instead learning a path using the trie and narrowing the steps in that manner.



## Results
1. The newly created IDs leave zero collisions. The model trains end to end without mapping one ID to two trails. All generated IDs returned in the correct structural format I designed. This is one of my first successes in which I have no issues with the T5 model generating my design.

The retrieval quality is poor. Failure is expected and is the only route for improvement. 

## Notes
Dealing with only BM25 will affect my research with how my model improves GENIR
More Transformer models to train the DocIDs would be best.

