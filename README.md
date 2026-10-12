# Data Science Toolbox: Formative Sprint 0 (Data Review and Group Work Primer)

University of Bristol, Data Science Toolbox. Our group reviewed resources for doing data science in sports analytics. Each member analysed a different dataset.

## Project Group

* Luke D: Formula 1 tyre strategy (Python, FastF1)
* Thomas F: Premier League match modelling and bookmaker odds (Python, penaltyblog)
* Morgan L: Premier League scoring and added time (R, tidyverse, BSDA)

This project has a 33/33/33 equity split between the three project members.

## Reading order and requirements

All report content is in the directory:

* report/

Each file is the work of the member named in its filename. The files can be read in any order, but this is the suggested order:

* 01-LukeD_F1_TyreStrategy.ipynb: does tyre make-up predict winning in dry F1 races? (EDA, permutation tests, logistic and conditional logit models). The code requests the 2022 season, but the executed output covers 38 races; a note in the notebook explains why.
* 02-LukeD_F1_FastF1Example.ipynb: the FastF1 gallery example [*Tyre strategies during a race*](https://docs.fastf1.dev/gen_modules/examples_gallery/plot_strategy.html) that the F1 analysis starts from.
* 03-ThomasF_PremierLeague.ipynb: the penaltyblog [end-to-end example](https://penaltyblog.readthedocs.io/en/latest/models/example.html) (Dixon-Coles model on three Premier League seasons), extended with visualisations of bookmaker margins, team strengths, scoreline probabilities and customer returns by odds band.
* 04-MorganL_PremierLeague.Rmd (knitted: 04-MorganL_PremierLeague.pdf): was the high-scoring 2023-24 Premier League season driven by longer added time and more goals after 90 minutes? Reproduces the analysis in [Akshat29-shah/epl-analysis](https://github.com/Akshat29-shah/epl-analysis) (replacing its z-test with Welch's t-test), extends it to cards and substitutions, relates the scoring change to Over 2.5 and BTTS betting markets, and extends to 2024-25 and 2025-26 using Football-Data match files with Bet365 odds. It reads its data from MorganL/.

Executed notebooks with outputs, and the knitted PDF of the R Markdown file, are included for convenience, since the data download for the F1 notebook is rate-limited.

Requirements:

* Python: `fastf1`, `penaltyblog`, `pandas`, `numpy`, `scipy`, `statsmodels`, `matplotlib`, `seaborn`
* R: `tidyverse`, `BSDA`, `rmarkdown`

## Evidence

Our individual working is shown in our own directories:

* LukeD/: F1 notebooks and the per-driver race strategy table (race_strategies.csv)
* ThomasF/: penaltyblog notebook and the downloaded match data
* MorganL/: R Markdown analysis, knitted PDF, and the match, event and Football-Data CSV files it uses

## Reflections

Reflections are in the folder:

* reflection/
  * LukeD_Reflection.md (and LukeD_Reflection.pdf)
  * ThomasF_Reflection.pdf
  * MorganL_Reflection.pdf
