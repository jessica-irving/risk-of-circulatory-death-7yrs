# Estimating seven-year risk of death from circulatory causes in those aged 50+

In this notebook I compare the performance of two prototype survival models, **Cox Proportional Hazards** regression and **Random Survival Forests**, at estimating seven-year risk of death from circulatory causes. I train these models on data from individuals entering the cohort from 1995 to 1998, with the test set (14% of the total data) comprising all individuals from 1999 to 2003.

From a few simple predictors it was possible to build a classifier for predicting risk of death from a circulatory disease at seven years that performed well in external temporal validation (see Figure 1).

These predictors were:

`age`: Age at entry to the cohort

`sex`: Participant sex

`kl_sum`: Summed kappa and lambda values from serum free light chain

`kl_ratio`: Ratio kappa:lambda

`kl_interaction`: `kl_sum` * `kl_ratio` to account for an interaction effect

`mgus`: Whether the subject had been diagnosed with monoclonal gammapothy (MGUS)

`creatinine`: Serum creatinine

**Figure 1.**
![Comparison between Cox proportional hazards and random survival forest model](https://github.com/jessica-irving/risk-of-circulatory-death-7yrs/blob/main/CPH%20vs%20RSF%20comparison.png?raw=true)

Strikingly, the CPH and RSF models were stronger at predicting in the short term and long term respectively, and therefore might pose different use cases. Perhaps the models' complementary use cases could also be exploited via an ensemble modelling method. Both models were roughly equivalently well-calibrated. Interestingly, the models seem to disagree on which features aside from age are important.

One thing to note is that there were far fewer circulatory death events in the validation set than the derivation set. More investigation is needed to establish whether this has inflated estimates of model performance.

### Limitations

Limitations and next steps are discussed in full in the analysis notebook. These namely relate to:
- Evidence of competing risks (left censoring)
- Time-varying coefficients
- Data leakage in feature importance ranking
- The need to calculate more fine-grained metrics
