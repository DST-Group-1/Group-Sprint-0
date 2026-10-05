# Individual Reflection: Data Science Toolbox, Formative Sprint 0

**Luke D**

## Fit: area and goals

Our group chose sports analytics. Each of us took a different dataset, found the resources that exist for analysing it, ran their example code and extended it. I worked on Formula 1 using the FastF1 Python package ([FastF1 documentation](https://docs.fastf1.dev/)). Thomas F analysed Premier League data using penaltyblog ([penaltyblog documentation](https://penaltyblog.readthedocs.io/en/latest/index.html)). Morgan L's contribution had not been uploaded when I wrote this.

My question was whether tyre strategy is associated with winning a race. I started from the official FastF1 tyre-strategy gallery example and extended it into an inferential analysis. Three decisions shaped the project. I restricted the data to the 2022 season because the F1 data server rate-limited my downloads. I kept only dry races, because compound choice means something different in the wet. I compared drivers within each race rather than pooling races, because track, weather and safety cars change what a "good" strategy is.

## Depth: results and the mathematics

Grid position dominates. The within-race Spearman correlation between grid position and finishing position was about 0.70, and pole-sitters won roughly 61% of dry races. The Hard-tyre starters initially looked unusual, but this was confounding: back-of-grid drivers disproportionately start on Hard. When grid position is included, the apparent effect reverses, which is a Simpson's paradox. The correlation between number of stops and result is probably reverse causation, since drivers running badly are more likely to be forced into extra stops. My conclusion is that, once grid position is controlled for, I found no evidence that tyre make-up predicts winning.

The final model was a conditional logit with race fixed effects. Each race has exactly one winner, so I model that winner as a choice among the drivers in the race. Driver *i* in race *r* has a score $x_{ir}^\top\beta$, and the probability of winning is a softmax over the field:

$$P(i \text{ wins race } r) = \frac{\exp(x_{ir}^\top \beta)}{\sum_{j \in r}\exp(x_{jr}^\top \beta)}.$$

Any race-level term added to every driver's score cancels in the ratio. That is why this model absorbs race effects without estimating a parameter per race. Each $\exp(\beta_k)$ is an odds ratio for beating the others in the same race (McFadden, 1974). I consulted Claude Opus 5.5 when choosing this model, then ran and adapted the notebook myself. The adaptations were mainly to cope with rate limits and the data scope.

**Weaknesses.** The model has no driver or car effect, and car performance is the obvious unmeasured confounder. Grid position partly proxies it, so the grid coefficient is not a causal effect. Wins are rare events, so power is low. Teams must use at least two dry compounds in a race, which constrains the strategy variables. My executed output also covered 38 races rather than the 22 of 2022, because an old multi-season CSV was still in my data folder. I found this after running the analysis and should have checked the data scope before interpreting anything. Next time I would validate the data size and date range first, and add driver and constructor effects or use finishing position rather than just wins.

## Literature search and comfort zone

My literature search was weak. I relied on package documentation and a few tutorials, and I found no academic work on F1 strategy. The gallery example is descriptive and does not test anything, so I had to take the inferential step myself. A thorough search would have been in the sports-statistics literature on rank and choice models.

I am most comfortable in Python and I would like to learn more R, for example `clogit` in the `survival` package, which would have let me cross-check my model. To use these resources better I need more experience with discrete-choice and causal-inference methods, and more F1 domain knowledge, such as how safety-car timing affects strategy.

## Collaboration and group working

GitHub enabled us to work in parallel: each of us had a folder and a different dataset. It also limited us. I tried to commit my FastF1 cache and hit the 100 MB file limit. I learned that caches are regenerable derived data and belong in `.gitignore`, because git keeps every version of every file in its history. Because we used different packages with different data, we compared approaches only loosely. At the time of writing Morgan's part was missing, so we had less to compare, and I cannot yet describe the whole project. For next time I would agree a common structure, shared `requirements.txt` and earlier check-in points at the start.

## Evidence

My contribution is the F1 analysis notebook, including feature extraction, the dry-race filter, permutation tests, Spearman correlations, the logistic models and the conditional logit. It is in my folder and in the report folder.

## References

McFadden, D. (1974). Conditional logit analysis of qualitative choice behavior. In P. Zarembka (Ed.), *Frontiers in Econometrics* (pp. 105-142). Academic Press.
