# Week 10


## Goals
1. Build poster based on summer research for DREaM scholar workshop in Natick, Massachusetts.
2. Final corrections on Journal.

## Approach and Implementation

## Poster Creation
Filled the content template entirely from the paper's actual results rather than restating the abstract.
Included all three identifier variants, the full ablation table with hits at k, MRR, precision, and recall, the worked example, the error analysis finding, and the constrained decoding result.
Generated four figures: a pipeline diagram, an identifier anatomy breakdown, a hits at k line chart, and an MRR bar chart.
Wrote the connection statement bridging clinical trial catalog retrieval to space object catalog association, arguing they are structurally the same constrained retrieval problem over a fixed catalog with hard eligibility predicates.
Built the final poster at 48 by 36 inches, landscape, three-column layout, one color, one font, white background, with the figures placed per the layout plan.


## Results
The poster is finished. It bridges this summer's work to a space domain awareness audience. The layout is 48 by 36 inches, landscape, three columns, one color, one font, white background. Content is drawn entirely from verified paper results. It shows all three identifier variants side by side. It carries the full ablation table with hits at k, mean reciprocal rank, precision, and recall for each variant. It includes one worked example tracing a single trial through the identifier format from end to end. It states the error analysis finding: the model produces the correct semantic segments and fails on the arbitrary registration number. It states the constrained decoding result: restricting generation to valid identifiers eliminated invented identifiers entirely, while unrestricted generation produced no correct results at all. Four figures are embedded. A pipeline diagram showing the stages from trial text to retrieved identifier. An anatomy diagram breaking the identifier into its segments. A line chart of hits at k across the three variants. A bar chart of mean reciprocal rank. The closing panel states the transfer argument: matching a patient to a trial catalog and matching an uncorrelated observation to a space object catalog are the same retrieval problem, both requiring a query to resolve to exactly one entry in a fixed catalog under hard eligibility constraints.

## Notes
I started this summer not knowing what a differentiable search index was. I finished it having built one, broken it, measured it, and found the flaw in my own contribution before a reviewer did. 
I learned that research is the process of documentation and monitoring. Experimentation needs to be an experiment and it needs to be shown.
The biggest discovery was that he eligibility fields I built the design around are missing from most of the corpus. Age is unstated for about half of it and sex for nearly two thirds. So for most trials, the meaningful parts of the identifier collapse to placeholders and the design reduces to what it was replacing. This needs to be worked on. It is not a failure but the true trickiness that exists in this field. Clinical Trials and Patient documentation will not change any time soon. Man must adapt to the randomness of the world. Machine has yet to follow. 
I enjoyed myself under the direction of my mentor Dr. Sun and my near-peer mentor Supriya Kottam.

