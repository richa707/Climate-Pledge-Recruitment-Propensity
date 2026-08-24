# Climate Pledge Recruitment Propensity Model

A propensity-to-join model built for Amazon Worldwide Sustainability (WWS) to identify which companies are most likely to sign Amazon's Climate Pledge — and to prioritize recruitment outreach by combining that likelihood with each company's potential emissions impact.

## Problem

Amazon's Climate Pledge recruitment team needed a way to prioritize outreach across thousands of candidate companies, but the data had a hard constraint: only 5.9% of the 4,000+ candidate companies had a confirmed label (i.e., had already signed). Standard supervised classification struggles badly under this kind of severe label scarcity, since "unlabeled" doesn't mean "not interested" — it just means "hasn't signed yet."

## Approach

- **Data**: Firmographic data, emissions data (Scope 1/2/3), and sustainability disclosure signals pulled from CDP, SBTi, EV100/RE100, and EcoVadis for 4,000+ companies.
- **Modeling**: Framed this as a Positive-Unlabeled (PU) learning problem rather than standard binary classification, since only signatories are reliably labeled. Used PU Bagging with XGBoost as the base learner to estimate true propensity-to-join scores despite the missing/unlabeled negatives.
- **Validation**: Masked a subset of known signatories and measured how many the model could recover. The PU approach recovered 34 of 56 masked signatories, versus 26 for a standard XGBoost baseline trained without the PU correction — and surfaced 13 additional high-propensity prospects the baseline missed entirely.
- **Ranking**: Engineered a normalized composite impact score (percentile-ranked propensity × percentile-ranked emissions) to combine "likely to say yes" with "matters most if they do." Used this to segment a Top 100 prospect list into three recruitment quadrants.
- **Impact**: The three quadrants together represent 58.1B tCO2e of potential emissions coverage if recruited.

## Deliverables

- Segmented, ranked target list of top prospects
- Supporting dashboard/visualizations translating model outputs and feature importance into plain-language recommendations for a non-technical recruitment team

## Repo Contents

This repo contains the modeling and pipeline code only. Underlying company/emissions data and full model outputs are not included, since the source data is not mine to redistribute (and the output files were too large to check in). 

## Tech Stack

Python, pandas, scikit-learn, XGBoost, PU learning (bagging-based)

## Notes

Reach out if you'd like a walkthrough of the methodology or results, happy to share the full report/poster on request given the data sensitivity.
