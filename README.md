# feature-concrete

How concrete are the features people list for a word, compared with how concrete the word itself is? This project uses semantic feature listing data to look at the relationship between cue concreteness and feature concreteness, and at what else predicts how concrete a listed feature is (semantic distance, feature frequency, and position and surprisal within a chain of features).

Status: work in progress. Study 1 analyses are drafted and still changing.

## Study 1: semantic feature listing

Participants were given a cue word and listed features of it. All responses are kept, including idiosyncratic ones. Concreteness ratings for cues and features come from published norms.

Analyses in [analysis/study1_analysis.Rmd](analysis/study1_analysis.Rmd):

1. **Cue vs. feature concreteness.** Cue-level correlation and regression of mean feature concreteness on cue concreteness.
2. **Hierarchical mixed models** (cue-pair level). Predictors are added in steps (cue concreteness, semantic distance, feature frequency, distance x frequency) and each step is tested with likelihood ratio tests.
3. **Participant-level models.** The same hierarchy on the full long-form data with random intercepts for cue and participant, plus a random slope of (centered) cue concreteness by participant.
4. **Chaining and surprisal.** Treating each answer as an ordered chain of features, tests whether concreteness drifts with position in the chain and whether the transition surprisal between consecutive features predicts concreteness, controlling for word frequency.

Still to do: embedding-based semantic distance, corpus-based (for example OpenSubtitles) collocational frequency and next-word probabilities, and the remaining studies.

## Repository structure

| Folder | Contents |
|---|---|
| `data/` | Input data (below) |
| `analysis/` | R Markdown analysis scripts |
| `manuscript/` | Manuscript files (empty for now) |

### Data

| File | What it is | Source |
|---|---|---|
| `data/08_words.csv` | Long-form feature listing data: one row per participant, cue, and feature word (with `position` in the answer). Participant ids are hashed. | Reprocessed feature listing data (Buchanan et al., 2019 word norms) |
| `data/concreteness_norms.csv` | Concreteness ratings (1 = abstract, 5 = concrete) plus SUBTLEX frequency | Brysbaert, Warriner, & Kuperman (2014) |
| `data/lancaster_norms.csv` | Mean ratings on 11 sensorimotor dimensions, used to compute cue-feature distance | Lynott, Connell, Brysbaert, Brand, & Carney (2020) |

## Reproducing the analyses

Requires R with the `tidyverse`, `lme4`, `lmerTest`, and `rmarkdown` packages. From the `analysis/` folder:

```r
rmarkdown::render("study1_analysis.Rmd")
```

The participant-level and chaining models fit several hundred thousand rows each and take a few minutes. The rendered HTML is not tracked in git.

## References

- Brysbaert, M., Warriner, A. B., & Kuperman, V. (2014). Concreteness ratings for 40 thousand generally known English word lemmas. *Behavior Research Methods, 46*, 904-911.
- Buchanan, E. M., Valentine, K. D., & Maxwell, N. P. (2019). English semantic feature production norms: An extended database of 4436 concepts. *Behavior Research Methods, 51*, 1849-1863.
- Lynott, D., Connell, L., Brysbaert, M., Brand, J., & Carney, J. (2020). The Lancaster Sensorimotor Norms: Multidimensional measures of perceptual and action strength for 40,000 English words. *Behavior Research Methods, 52*, 1271-1291.
