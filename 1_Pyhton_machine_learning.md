# [![My Skills](https://skills.thijs.gg/icons?i=py)](https://skills.thijs.gg) machine learning


Reinforcement learning
- https://towardsdatascience.com/reinforcement-learning-101-e24b50e1d292
- https://www.wikiwand.com/en/Reinforcement_learning
- https://deepsense.ai/what-is-reinforcement-learning-the-complete-guide/

Other links
- https://harvard-ml-courses.github.io/cs181-web/recaps/lec1

ML class links
- https://ml-ops.org/content/mlops-principles
- https://chrisalbon.com/
- https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/
- http://scott.fortmann-roe.com/docs/BiasVariance.html
- Examples
	- https://scikit-learn.org/stable/auto_examples/model_selection/plot_underfitting_overfitting.html
	- http://www.navan.name/roc/
	- https://scikit-learn.org/stable/auto_examples/cluster/plot_cluster_comparison.html
	- https://pair-code.github.io/understanding-umap/
- All models have tendency to overfit to some extent: “If you torture the data long enough, it will confess.” (Nobel Laureate Ronald Coase)
- Logistic regression: “All else being equal, if your income had been $20,000 higher you would have been granted this particular mortgage.”
- KNN: “We declined your mortgage application because you remind us of the Smiths and the Mitchells, who both defaulted.”
- https://towardsdatascience.com/the-surprising-behaviour-of-distance-metrics-in-high-dimensions-c2cb72779ea6
- https://towardsdatascience.com/t-distributed-stochastic-neighbor-embedding-t-sne-bb60ff109561
- https://towardsdatascience.com/an-introduction-to-t-sne-with-python-example-5a3a293108d1
- https://towardsdatascience.com/neural-network-embeddings-explained-4d028e6f0526
- https://pair.withgoogle.com/guidebook/
- https://towardsdatascience.com/tsne-vs-umap-global-structure-4d8045acba17
- https://www.forbes.com/sites/gilpress/2016/03/23/data-preparation-most-time-consuming-least-enjoyable-data-science-task-survey-says/
- https://explained.ai/gradient-boosting/L2-loss.html
- https://medium.com/swlh/gradient-boosting-trees-for-classification-a-beginners-guide-596b594a14ea
- https://towardsdatascience.com/gradient-boosted-trees-for-classification-one-of-the-best-machine-learning-algorithms-35245dab03f2
- https://explained.ai/gradient-boosting/descent.html
- https://towardsdatascience.com/catboost-vs-light-gbm-vs-xgboost-5f93620723db
- https://mksaad.wordpress.com/2019/12/21/stacking-vs-bagging-vs-boosting/
- https://rikunert.com/smote_explained
- https://realpython.com/k-means-clustering-python/
- https://github.com/jermwatt/machine_learning_refined
- https://www.analyticsvidhya.com/blog/2016/03/complete-guide-parameter-tuning-xgboost-with-codes-python/
- https://kiwidamien.github.io/how-to-do-cross-validation-when-upsampling-data.html
- https://www.kaggle.com/getting-started/159643
- https://stats.stackexchange.com/questions/288095/what-algorithms-require-one-hot-encoding
- https://stats.stackexchange.com/questions/244507/what-algorithms-need-feature-scaling-beside-from-svm
- https://towardsdatascience.com/5-smote-techniques-for-oversampling-your-imbalance-data-b8155bdbe2b5
- https://towardsdatascience.com/catboost-vs-light-gbm-vs-xgboost-5f93620723db
- https://towardsdatascience.com/a-novel-approach-to-feature-importance-shapley-additive-explanations-d18af30fc21b
- https://towardsdatascience.com/a-novel-approach-to-feature-importance-shapley-additive-explanations-d18af30fc21b


True positive rate = Recall = Sensitivity
True negative rate = Specificity = TN / (TN + FP)
False positive rate = 1 - Specificity

```
# Xgboost, lightgbm
conda install -c conda-forge xgboost lightgbm

# catboost gradient boosting 
conda install -c conda-forge catboost 

# tensorflow neural networks (pydot needed for some plots in tensorflow) 
conda install -c conda-forge tensorflow 

# shap interpreting ML models 
conda install -c conda-forge shap 

# spacy, nltk text analysis 
conda install -c conda-forge spacy 
conda install nltk 

# aequitas Bias and Fairness Audit Toolkit 
pip install aequitas 

# yellowbrick machine learning visualization 
conda install -c districtdatalabs yellowbrick
```

- The general rule is balancing, scaling, selection
