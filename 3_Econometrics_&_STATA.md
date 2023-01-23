# Econometrics
          
In this section I gather the relevant books and general resources on Econometrics, using either R or STATA, which I found relevant in my work or learning journey.

## 📖 books
- [Introduction to Econometrics with R](https://www.econometrics-with-r.org/index.html)
- [R Companion to Real Econometrics](https://bookdown.org/carillitony/bailey/)
- [The Effect Book](https://theeffectbook.net/ch-EventStudies.html?panelset=stata-code) (both STATA and R)
- [Principles of Econometrics with  R](https://bookdown.org/ccolonescu/RPoE4/)
- [Causal Inference: The Mixtape](https://mixtape.scunning.com/) (non-code-based)
- [Causal Inference for The Brave and True](https://matheusfacure.github.io/python-causality-handbook/landing-page.html) (Pyhton)
- [Causal Inference: What If (the book)](https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/): companion [Python repo](https://github.com/jrfiedler/causal_inference_python_code)


## ```STATA```
General guides to using STATA useful for both begginer and advanced users:
- [STATA (and R) tutorials](https://errickson.net/workshops.html): matching with R;  regression and mixed effects modeling with STATA
- [STATA guide](https://wlm.userweb.mwn.de/Stata/): general STATA tips
Specific tasks/ resources:
- [Decomposing, probing, and plotting interactions in STATA](https://stats.oarc.ucla.edu/stata/seminars/interactions-stata/)
- [Causal machine learning for Econometrics: causal forests](https://towardsdatascience.com/causal-machine-learning-for-econometrics-causal-forests-5ab3aec825a7)
- [Propensity score matching](https://www.ssc.wisc.edu/sscc/pubs/stata_psmatch.htm) and complementary resources: [#1](https://www.stata.com/meeting/italy14/abstracts/materials/it14_grotta.pdf) [#2](https://rpubs.com/buidiengiau/psm-stata) [#3](https://medium.com/@thestataguide/propensity-score-matching-in-stata-ba77178e4611)
- [labmask](http://fmwww.bc.edu/RePEc/bocode/l/labmask.html): give labels to the different values of one variable

### Snippets
[Handle too many values when using encode](https://www.statalist.org/forums/forum/general-stata-discussion/general/1359717-error-message-too-many-values-when-using-encode-command)
```stata
egen long artist_code = group(artist_name)
```

Create a list of variables
```stata
local explanatory_variables "var1 var2 var3"
```

## <img height=50 src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/rstudio/rstudio-original.svg" />
- Regression model diagnostics:
  - [Collinearity, model fit and variable contribution](https://cran.r-project.org/web/packages/olsrr/vignettes/regression_diagnostics.html)
  - [Linear regression assumptions and diagnostics](http://www.sthda.com/english/articles/39-regression-model-diagnostics/161-linear-regression-assumptions-and-diagnostics-in-r-essentials/)
  - [Checking OLS assumptions](https://www.rpubs.com/elliottb90/olsassumptions)
- [Fixed/ random effects models](https://rstudio-pubs-static.s3.amazonaws.com/372492_3e05f38dd3f248e89cdedd317d603b9a.html)
- [An introduction to ‘margins’](https://cran.r-project.org/web/packages/margins/vignettes/Introduction.html?utm_source=pocket_mylist)
- [Difference-in-differences (DiD) package](https://bcallaway11.github.io/did/)
- [Count data models](https://stats.oarc.ucla.edu/stata/seminars/regression-models-with-count-data/)
- [Methods to deal with zero values in logarithmic transformation](https://aosmith.rbind.io/2018/09/19/the-log-0-problem/#generate-log-normal-data-with-0-values)

## <img height=50 src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" />
- [Difference-in-differences (DiD) package](https://differences.readthedocs.io/en/latest/getting_started/index.html)
- [Generalized linear models](https://towardsdatascience.com/scikit-learns-generalized-linear-models-4899695445fa)
- [Packages for causal inference](https://towardsdatascience.com/4-python-packages-to-learn-causal-analysis-9a8eaab9fdab)

## 🎓general resources
- [Matching Methods for Causal Inference: a Machine Learning Update](https://humboldt-wi.github.io/blog/research/applied_predictive_modeling_19/matching_methods/)
- [Research methods](https://clas.ucdenver.edu/marcelo-perraillon/teaching/health-services-research-methods-i-hsmp-7607): for empirical researchers (examples in STATA) by Professor [Marcelo Coca Perraillon](https://clas.ucdenver.edu/marcelo-perraillon/)
- [Econometrisc Academy](https://sites.google.com/site/econometricsacademy/home?authuser=0): general learning resources (on both STATA and R)
- [Applied empirical methods](https://github.com/paulgp/applied-methods-phd): econometric methods course for empirical research
- [Panel data econometrics](https://sites.google.com/view/christophe-hurlin/teaching-resources/panel-data-econometrics?utm_source=pocket_mylist): course on panel data
- Courses taught by [Professor David Childers](https://donskerclass.github.io/):
  - [Causal Econometrics](https://donskerclass.github.io/CausalEconometrics.html) (non-code-based)
  - [Forecasting for Economics and Business](https://donskerclass.github.io/Forecasting.html) (non-code-based and R)
  - [Econometrics](https://donskerclass.github.io/EconometricsII/Econometrics.html) (non-code-based and R)
- [Propensity score matching in Python](https://towardsdatascience.com/psmpy-propensity-score-matching-in-python-a3e0cd4d2631)
- [Why can R2 be negative and what does it mean?](https://stats.stackexchange.com/questions/183265/what-does-negative-r-squared-mean)
