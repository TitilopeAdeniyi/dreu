# Week 8


## Goals

This was the week of the conference submission, so the week's goals are set by the deadline. Several goals will be met and they will happen in this order.
1. Build trie from valid DocID set and constrain beam to it.
2. Reread papers on GENIR literature (DSI, GenRet, GenIR Survey)
3. Audit evaluation metrics to produce results for poster and paper.
4. Rewriting Session I dense retrieval baseline running end to end.
5. Finish Session II for Conference Paper.
6.  Replace placeholder document identifier with real one, and final collision-free check
7.  Train on the GPU cluster
8.  Draft, audit and submit conference paper.
## Approach and Implementation
The DocID's from the TrialGPT were remapped to my crafted semantic-aware framework. 

Final DocID design
- Designed Semantic-Aware identifier around three ideas: a semantic prefix from hierarchical clustering of trial embeddings, an  eligibility segment encoding age band, sex, and healthy volunteer status, and a numerical tail from NCT ID number.
- Established that the eligibility segment is the main contribution to this project and is absent in the generative information retrieval genre.
- Eligibility information exists in the eligibility section of the raw records. Phase, study type and enrollment reside in a separate design section.
- Changed the specialty field from one specialty band to a multiple bit-mask. Around 18% of trials belong to more than one category.
- Changed age field from three coarse buckets to encoded numeric boundaries.
- Extended the numeric tail from five characters to seven/
- Found and fixed false positive specialty pattern.
- Restricted specialty extraction to the title plus the first 300 characters of inclusion criteria.

  ### Writing Paper
  - Wrote an analysis pass over all three identifier versions counting unresolved fields, to quantify the unknown placeholders I had been seeing in outputs.
  - - Drafted the paper from the verified output files only, which forced me to correct several claims that I previously didn't think about.
 - Computed exact significance tests from per-patient hit vectors.
- Ran repeated adversarial review passes on the draft, deliberately harsh, looking for what a hostile reviewer would find first
## Results
The revised identifier scheme produced zero collisions across all 26,162 trials. Collision analysis confirm that three character tails collide at this corpus size. Four is better, and five is safer. But, testing at corpus scale found 2,444 real collisions at the five character tail. The tail was extended to seven characters . The design notes a fifteen character identifier. The code built a 24 character one. The code is correct. Training completed on GPU. Embeddings were produced for the full corpus as a 26,162 by 768 float32 matrix with an aligned identifier key. The encoder check passed. The pipeline runs regardless of working directory. The Session I baseline completed. It scored 200 patients profiles against 6,599 trial criteria rows across three embedding models. Top-five ranks were produced. Labeling switched to official judgements and eight synthetic profiles were reassigned to eligibility boundary cases. Field completeness was quantified across all three schemes. In the earlier scheme 34.8 percent of trials matched no specialty and 74.9 percent had a fully unknown age range. In the revised scheme those figures are 19.6 percent and 51.2 percent. Sex is 62.8 percent unresolved in both, since both use the same extraction logic. These figures imply a confound. If age is unstated for half the corpus and sex for nearly two thirds, the semantic segments collapse to placeholders for most trials, and any measured improvement could be concentrated in the minority where fields resolve.

## Notes

Seven days were worked with no break, two of them overnight.
Conference Paper completed.
