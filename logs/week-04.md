---
layout: post
title: "Week 4: One month into Generative Information Retrieval "
date: 2026-06-07
---

## Goals

Define what Generative Information Retrieval is. GenIR utilizes AI to replace traditional document ranking lists by generating the relevant document identifiers that match a query. No sorting, no indexing, no instructions to find the ranked list. The model itself is the index and the retriever.

What are the steps of GenIR for DocIDs?

1. DocID design
2. Indexing, where the model memorizes the corpus/training data  through document-to-DocID training pairs
3. Query encoding
4. DocID generation via beam search
5. Constrained decoding, where a prefix trie restricts the model so it can only produce IDs that actually exist
6. Ranking by beam scores

This is the broad map of how I will need to go about my research. I am to finish assembling the Session I dense retrieval baseline so it would be ready for manual evaluation next week.
I started naming my practice data AAA, BBB and so on leading to many copies I could not keep up with. Therefore I will be implementing better naming practices to circumvent this issues.
Research also involves adopting new practices that better promote easier workflow. 
---

## Approach and Implementation

### Recovering AAA.py

The week started with a setback. My baseline script `AAA.py`, which lived at `~/TestTrials/AAA.py` on the Knuth server, was lost because I couldn't keep up with the names and permanently deleted it. I chose names for the pure convenience for the terminal. I did not have a current backup, I had it all on the terminal and I've learned from this setback. I rebuilt it from an old version of the code plus the output file it was supposed to produce, working backward from what the results looked like to what the script had to be. 

The reconstructed script encodes synthetic patient profiles and clinical trial criteria with three models:

| Model | Checkpoint | Dim |
|---|---|---|
| SBERT MiniLM | `all-MiniLM-L6-v2` | 384 |
| PubMedBERT | `pritamdeka/S-PubMedBert-MS-MARCO` | 768 |
| SapBERT | `cambridgeltl/SapBERT-from-PubMedBERT-fulltext` | 768 |

By computing cosine similarity, retrieves the top 5 trials per patient, and writes `manual_eval.csv` with columns `patient_id`, `diagnosis`, `model`, `rank`, `trial_index`, `trial_title`, `score`, `relevance`, `notes`. I kept up the practice of having and output txt file created for reading convenience. My terminal skills are getting better, but I still need to keep to my comfort zone or else I will lose data again.

Additonally, I cleaned up the output for scale. I plan to run this on up to 5,000 patients eventually, so hardcoded counts had to go. The profile table now prints the first 5 rows and then a dynamic "and N more profiles" line, and the retrieval loop prints the first 5 patients and then continues processing silently. 
### Learning the GenIR paradigm

Classic Infromation Retrieval

```
query > encoder > compare against all documents > rank
```

The novel GEN IR workflow:

```
query > decoder > generate DocIDs directly
```

I worked through what this means for my own data. A patient profile like "62 year old female, HER2 positive breast cancer, prior taxane therapy" becomes the input, and the model generates a trial identifier as the output. The DocID can be the NCT number directly, or it can be a semantic ID that encodes structure, like `CLUSTER1-BRESCAN.62.F`. The semantic version gives the model something learnable instead of an arbitrary number to memorize. Using text and numbers seems like a good model to work with but it's very rough to begin with. How does one create a univerally understood Doc ID? Should Doc IDs speak to the scientists, programmers, both or a new third party? 

Additonally, does the model invent new doc IDs, or output ones that already exist? The straightforward answer is that DocIDs are pre-assigned by the developer(My role) from document metadata before training ever starts, and the model learns to recall the correct pre-existing ID for a query. It works like a seasoned medical biller or a wise librarian. They know their category well. I need to keep this in mind, The model should emulate the world's best librarians combined. 



### Assembling the Session I pipeline

The current product of my Session I progress
| Script | What it does |
|---|---|
| `download_trials.py` | Fetches raw trial JSON from ClinicalTrials.gov |
| `parse_trials.py` | Raw JSON to `combined_parsed.csv` |
| `normalize_trials.py` | Cleaned criteria text to `combined_normalized.csv` |
| `baselineNeuralRetrieval.py` | Dense retrieval, top 5 trials per patient by cosine similarity |
| `generate_patient_profiles.py` | 200 synthetic patients: 180 women's health, 20 male control, fixed seed |
| `append_trials.py` | Adds trial titles to the evaluation sheet |
| `evaluation_metrics.py` | Precision@5 and Recall@5 |
| `run_pipeline.py` | Ties all the steps together |
| `parse_trec_topics.py` | Manual parser for the TREC topics XML |

No real patient data yet, It's only as placeholder. 

---

## Successes

- Reworked my AAA .py file 
- Improved my output script.
- The full Session I pipeline runs end to end: download, parse, normalize, retrieve, score.
- `generate_patient_profiles.py` produces a reproducible 200-patient set with per-profile age and sex constraints. Fixing the random seed means anyone can regenerate my exact cohort.
- I understand the GEN IR literature better. 
- I name my files better.
- I keep a back up of all my files locally, incase of another accidental deletion

## Failures

- AAA.py got deleted 
- The `ir_datasets` library failed on a checksum mismatch for the TREC Clinical Trials data, and I lost time before accepting it was not going to work. 
- My first pass at the GenIR material was too abstract to hold onto. The literature leads into too many rabbit holes I can't cover at once. Very dry.
- The baseline still uses only three models. BM25 and ClinicalBERT are missing, which means I have no lexical control to compare the neural models against yet. Will work on this later.

---

## Results

The baseline is assembled and waiting on evaluation. The corpus is curated, the 200 patient profiles exist, the three embedding models run end to end, the `manual_eval.csv` labeling sheet is set up on the TREC style 0/1/2 relevance scale, and every run now logs itself. Next week is the actual evaluation, where I find out which model retrieves the most clinically relevant trials.

