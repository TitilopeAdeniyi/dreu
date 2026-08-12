.# Week 7


## Goals
We are back to working on the trainer. Basic Seq-To-Seq T5. Train. Look at results. Change into a new direction and retrain. Review results, rinse and repeat. I am getting used to having poor results, but I am glad to have results. 
1. No Synthetics Patients, Using TREC 2021 Trials patients. That problem is done.
2. Fixed T5 on GPU. I had that issue fixed with a small test, so training will take 15 minutes.
3. The DocID is from Cluster from PubMedBert, Specialty, Age Band, Gender/Sex/Health Volunteer, and NCT Trial to fulfill unique DocID requirement.
   

## Approach and Implementation
Three things to work on, the data, the training model and the DocID. Conversion to the semantic docID was easily. I just use converter script that assigned the the clusters to the trial docs from the TriaLGPT files, then created a new version of the documents with the semantic ids. The old version used the arbitrary DocIDs (001, 002,..., .etc), mine use (Cluster-Specialty Bit Mask- Age - Sex- NCT Tail ). A small change, and something I can feel confident as my own contribution. 

## Results



## Notes


