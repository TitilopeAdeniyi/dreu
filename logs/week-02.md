---
layout: post
title: "Week 2: Current Climate of Generative Information Retrival"
---

## Goals
I played around with pulling trials on my local computer and seeing the entire format and needed information for eligibility matching. Most of the information is left blank after look through numerous examples and the important parts are 3 central areas: age, gender/sex, and inclusion/exclusions. The job is easier than it looks. Age and Inclusion/Exclusion might not be mentioned but gender/sex is always there. These three areas are the top priority. 

Additionally, I need to brush up on Generative retrieval. W
Questions to keep me focused: 
What is Information Retrieval?
How does Generative IR enhance the field?
Why is GEN IR needed in place of the current state of Information Retrieval?
Can humans and current algorithms handle every case for patient trial matching?

I do not need to answer these questions but to keep them in mind going through papers.
## Approach/Implementation
Papers I've collected to read: 
"Differentiable Search Index"
"From Matching to Generation: A Survey on Generative Information Retrieval" 
Concepts I will look into:
Doc ID design
Concepts I will not look into:
RAGs 

Document Identifier (DocID) design
# Results
Everything and anything I needed to know about GEN IR was in Generative Retrieval Survey. No longer are we using search algorthms to make sparse retrvials and exact keyword-matching. Nor can we rely simply on dense retrival. The famous example: drug resistant and resistanct drug may look the same through tradtional IR algorithms but they are majorly different things and is a fatal mistake to confuse the two. 
I'm still having a hard time understanding GEN IR, but I do understand that we, people, do none of the matching, the LM is trained on already matched pairs (linked ?) to a DOC ID. After training, the LM will take patient data and produce a DOC ID or list of DOC ID it was trained on to match on patterns produced on its training. Most of the papers I've read have diagrams explaining GEN IR, however I have the hardest time following them. 
I am still in the reading and writing notes stage, issues, frustrations and troubles only mean I am following the path many have taken to understand this subject. I am truely in the company of my peers. I've achieved my goals being that I am taking in all this new information and forming my own conclusions. 
 These are my current thoughts and I hope to see major improvement as the weeks follows. 
