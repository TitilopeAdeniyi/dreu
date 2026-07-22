---
layout: post
title: "Week 3: Baseline Attempt 1"
---
## Goals
First, I will continue reading and collecting papers (Thank you Notes LM)
Second, I need some code. 
My reading took me back to the beginnings of IR: who made what information retrieval is today , and who is building generative IR now. Particularly,  The SIGIR 2024 workshop splits GEN IR into four pillars: generative document retrieval, grounded answer generation, generative recommendation, and generative knowledge graphs.
I am focused on the first pillar only, but the others were intersting to know in mind. I had a baseline neural retrieval jupyter notebook that ran on my local machine. I needed it running on Knuth. 
It did not run on the Knuth, so going further I will only be creating .py files


## Approach/Implementation
I read about traditional or "classic" Information retreival pioneers.  Classical IR big names: Salton, Spärck Jones, Robertson. Their work is the foundation everything else sits on. Whatever I thought, they have it published and anything I didn't they've already come up with. I've taken a few papers and books from these indiviuals I will dive into at another time. GEN IR is suprisingly young, so its figures are recent: Metzler, Tay, Lewis. Reading from them made me realize, that the goal isn't about matching pairs, but generating. Something that sounds synomonous when spoken, but wildy different when coding.

In order to start the full coding process, I moved completely to the server. I converted my Jupyter notebook into a Python script, BBB.py, and put it in ~/TestTrials on Knuth. The name was simply a place holder as I got used to using WinSP and the Knuth server, but the script matches synthetic patient profiles against trial eligibility text using SBERT, PubMedBERT, and SapBERT for now. ClinicalBERT, BioBERT, TF-IDF, and BM25 planned next once the format is running smoothly. I redirected all output to out.txt with a so I keep a record. Knuth is terminal heavy and it's easier to review the results in a notepad.txt then constantly scrolling. It's not a perfect situation and pipeline, but it is a working one. 

## Results
The conversion was a fight.Juypter notebook is extremely powerful resource, but not for this project.The Knuth server and countless restrictions presented made simple python the way to go. 
CUDA isn't working for me, but that's all a part of the learning process. I have code written, notes and papers to read. 
**Scripts and programs**

What succeeded:
- BBB.py — notebook converted into a working server script; baseline retrieval runs on Knuth (on CPU).
- Tee output to out.txt — dual console and file logging.
- retrieval_results.csv — matches saved to file.
- Per-patient model comparison table  best trial and score per model, first five patients. Good Data tracking 
- Using python only
- Keeping it simple and utilizing what I have. Pen and Paper, Brainstorming then coding.
What failed:
- GPU access /CUDA rep, will resolve later but not now
- Don't use jupyter notebook, does not work on knuth server.

