---
layout: post
title: "Week 5: Result Harvest"
date: 2026-06-14
---

## Goals

Ran the manual evaluation of the dense retrieval baseline and get some numbers. 
If the results are good, I'm on the right track. If the results are bad, I'm on *a* track. The best position is that after hours of troubleshooting, the code ran successfully and produced some results. 
Dr. Sun has been helping me along the way with good resources and giving the feeback I need. This all will be written into a paper, so I need to keep experimenting. The best thing about Dr. Sun is that he is always encouraging me through my progress and I can always go to him for questions, advice and concerns. It keeps me on track and I'm thankful to have a seasoned researcher aiding me.

---

## Approach and Implementation

### Expanding the baseline to five models

I've added ClincalBERT and BM25 as a control, and another BERT to produce more results.

| Model | Role |
|---|---|
| BM25 | Lexical baseline |
| SBERT MiniLM | General-domain control |
| PubMedBERT | Clinical baseline |
| SapBERT | Clinical baseline |
| ClinicalBERT | Clinical model |

BM25 uses term-frequency scaling and typically scores from 0 up past 30, while the neural models produce cosine similarities bounded between 0.0 and 1.0. Those two ranges can never appear in the same output section due to false correlations. Therefore every report I generate now keeps lexical and cosine scores in separate blocks.

### Restructuring the project

I've been constantly creating back up and logs to the point that I've become more confused on what is the back up and what is the real testing folders. Thus, the flat `TestTrials/` directory has became a real project. Everything moved into `SummerSession1/` with subfolders `scripts/`, `raw/`, `processed/`, `patients/`, `eval/`, and `output/`. All paths are now resolve through `os.path.join(script_dir, "../subfolder/file.csv")` so a script runs the same no matter what directory I launch it from. When creating backup and copies, the path code lines always caused the most errors, so this needed to be resolved.

### The manual evaluation


I labeled `manual_eval.csv` following the TREC Clinical Trials track methodology: 0 for not relevant, 1 for partially relevant, 2 for eligible. `evaluation_metrics.py` then scored Precision@5 per patient and per model. The results:

| Model | Avg P@5 |
|---|---|
| SapBERT | **0.58** |
| SBERT MiniLM | 0.54 |
| PubMedBERT | 0.50 |

Avg P@5 stands for Average Precision at 5
Precision@5 asks a simple question about one patient: of the top 5 trials generated, how many were actually relevant? One count the relevant ones and divide by 5.

3 of the top 5 were relevant > Precision@5 = 3/5 = 0.60
5 of 5 relevant > 5/5 = 1.00 (bullseye)
0 of 5 relevant > 0/5 = 0.00 (a total miss)

The finding: PubMedBERT scored lowest despite producing the highest raw cosine scores. Similarity  does not track clinical relevance however.Like humans, a model can be confident and wrong at the same time. Confidence and Correctness are aspects I will need to extend on when writing my paper and reporting my results. Like these results, i could be confident and wrong at the same time too. 

### The Worst Patients discovery

I produced a "worst patients" analysis to see which patients every model failed on. The worst performers were dominated by Alzheimer's, diabetic retinopathy, and obesity, none of which are women's health conditions that my practice trails come from. Those patients were failing not because the models were bad persay, but because the corpus barely covers their conditions, and their failures were dragging down the whole evaluation. The quick fix was to regenerate the cohort as 180 women's health patients and 20 male controls, so the numbers measure retrieval quality from the domain I actually built the test dataset for. 

### What I looked up this week: the vocabulary

Going into the meeting with Dr. Sun, I filled in all the terminology I had been using loosely. I looked up and wrote one-to-two-sentence definitions for tokens, tokenizers, encoding, decoding, embeddings, and vectors, so I could explain what actually happens to a patient profile before it becomes a number. I looked up sparse retrieval versus dense retrieval, which is keyword matching against meaning-based vector matching. I looked up TF-IDF and BM25 as the classical lexical methods and cosine similarity . I looked up the difference between a bi-encoder and  looked up the context window and why it matters, since retrieved documents have to fit alongside the query. I looked up how SBERT, PubMedBERT, and SapBERT differ from each other by architecture, training data, and training objective, so my five-model lineup was a set of justified choices. I picked the first BERTs I could get my hands on and now I know their history, strengths and weaknesses

### Hardest Task of the week: The Mathatatics Behind Generative Retrieval


This was the hardest part of the week. The GenIR survey defines its whole method in formal notation, so I worked through the derivation symbol by symbol until I could explain each one in plain language. 

**1. Query-conditioned next-token probability**

$$P(d'_i \mid d'_{<i},\, q;\, \theta)$$

The probability the model assigns to the next DocID token $d'_i$, given the tokens already generated ($d'_{<i}$), the query $q$, and the model parameters $\theta$. This means for a probability to *depend on* $\theta$: two models with different parameters will assign completely different probabilities to the same token, for the same query, at the same step. $\theta$ is the entire trained behavior of the model rolled into one symbol.

**2. Joint generation probability**

$$P(d' \mid q;\, \theta) = \prod_{i=1}^{T} P(d'_i \mid d'_{<i},\, q;\, \theta)$$

The probability of generating the *entire* DocID sequence $d'$ of length $T$, found by multiplying together every individual token probability from the first step to the last. Because it is a product (the Big Pi $\prod$), one halted step crashes the whole score : if the model is unsure at even a single token, that small number multiplies through and lowers the probability of the complete DocID.

**3. Document relevance score**

$$\mathcal{R}(q, d) = P(d' \mid q;\, \theta)$$

This is THE most important equation of generative retrieval. The relevance of a document $d$ to a query $q$ is *defined as* the probability the model generates that document's DocID given the query. The generation probability **is** the relevance score. The top-k DocIDs with the highest $\mathcal{R}(q,d)$ become the retrieved results.

**4. Cross-entropy loss**

$$\mathcal{L} = -\sum_{i=1}^{T} \log P(d'_i \mid d'_{<i},\, q;\, \theta)$$

From what I gathered, the quantity the model minimizes as it learns. It is the negative sum of the log probabilities of each token in the ground-truth//absolutely true DocID. Minimizing this loss causes the model to assign high probability to the correct DocID's tokens.

This was one of the biggest hurdles and why consistant handwritten note-taking is important. What I could read on a screen and miss, took me hours of writing to understand.

### Big problem with DOC IDs

The NCT Trail IDs can not be used for training as they are, NCT00000002 doesn't hold any semantic meaning, but it could be used to create unique mappings. So we must move from this NCT design but refashion it. 


---

## Successes

- Real numbers EXIST. SapBERT at P@5 = 0.58, First set of results!
- The confidently-wrong PubMedBERT gets a gold star for participating in this experiment. Not every Medically trained BERT is the best BERT. 
- The five-model lineup has proper control baselines. Clearly there is an improvement from Classical Information Retrieval. If my research can simply prove that...
- I walked into my mentor meeting able to define most terms and understand the central equation. O couldn't do that two months ago.

## Weaknesses


- The Conference Deadline approaches.

---

## Results

Baseline: SapBERT 0.58, SBERT 0.54, PubMedBERT 0.5, 
It's time to train.
