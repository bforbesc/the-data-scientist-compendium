# <img height=50 src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" /> Python - Machine Learning

# 📖 books
- [Machine learning refined](https://jermwatt.github.io/machine_learning_refined/)
- [Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/): probably the most popular Python data science book, has a dedicated section on machine learning
- [Scikit learn official guide](https://scikit-learn.org/stable/user_guide.html)
- [Reinforcement Learning: An Introduction](http://incompleteideas.net/book/the-book-2nd.html): a book by the father of RL and his advisor
- [Matching Methods for Causal Inference: a Machine Learning Update](https://humboldt-wi.github.io/blog/research/applied_predictive_modeling_19/matching_methods/)

These are the code examples from two very good books which you can buy online:
- [Hands-on Machine Learning with Scikit-Learn, Keras and TensorFlow (code examples)](https://github.com/ageron/handson-ml2)
- [Introduction to Machine Learning with Python (code examples)](https://github.com/amueller/introduction_to_ml_with_python)

# 🔨 resources and tools
- [An introduction to machine learning with scikit-learn](https://scikit-learn.org/stable/tutorial/basic/tutorial.html): official scikit-learn (based) tutorial
- [Harvard CS181: Machine Learning](https://harvard-ml-courses.github.io/cs181-web/): lecture recaps and notes
- [Stanford CS231: Convolutional Neural Networks for Visual Recognition](https://cs231n.github.io/): lecture recaps and notes
- [Notes on data science & machine learning](https://chrisalbon.com/): ‼️incredible resource‼️ for Python snippets for data science and machine learning in general
- [Machine learning mastery](https://machinelearningmastery.com/start-here/#getstarted): another ‼️awesome resource‼️ with extremely complete reach from theory and practice of data science and machine learning
- [Guide to choosing the right algorithm/ estimator](https://scikit-learn.org/stable/tutorial/machine_learning_map/): visual tool to choose the appropriate machine learning algorithm for your specific problem
- [Dive into Machine Learning](https://github.com/metjush/dive-into-machine-learning): an (old but interesting) guide on machine learning and data science
- [Introductory course on Reinforcement Learning](https://www.davidsilver.uk/teaching/)

# 🤔 machine learning explained
Theoretical and practical explanations of machine learning concepts and ideas:
- [Machine learning algorithms: a visual guide](https://chart-studio.plotly.com/create/?fid=SolClover%3A40&utm_source=pocket_mylist#/)
- [Distance metrics in high dimensions](https://towardsdatascience.com/the-surprising-behaviour-of-distance-metrics-in-high-dimensions-c2cb72779ea6)
- Understanding ... 
	- [the bias-variance tradeoff](http://scott.fortmann-roe.com/docs/BiasVariance.html)
	- [underfitting vs. overfitting](https://scikit-learn.org/stable/auto_examples/model_selection/plot_underfitting_overfitting.html)
	- [ROC curves](http://www.navan.name/roc/)
	- [gradient boosting](https://explained.ai/gradient-boosting/): great and practical explanation of gradient boosting (and other concepts)
	- [the difference between clustering algorithms](https://scikit-learn.org/stable/auto_examples/cluster/plot_cluster_comparison.html)
	- [UMPA](https://pair-code.github.io/understanding-umap/)
	- [neural networks (from scratch)](https://www.youtube.com/playlist?list=PLQVvvaa0QuDcjD5BAw2DxE6OF2tius3V3)
	- [reinforcement learning](https://towardsdatascience.com/reinforcement-learning-101-e24b50e1d292)
	- [XGBoost (from scratch)](https://medium.com/analytics-vidhya/what-makes-xgboost-so-extreme-e1544a4433bb)
	- [structured learning](https://pystruct.github.io/intro.html)
	- [double machine learning for causal inference](https://towardsdatascience.com/double-machine-learning-for-causal-inference-78e0c6111f9d)
- [CatBoost vs. Light GBM vs. XGBoost](https://towardsdatascience.com/catboost-vs-light-gbm-vs-xgboost-5f93620723db)
- [Stacking vs. Bagging vs. Boosting](https://mksaad.wordpress.com/2019/12/21/stacking-vs-bagging-vs-boosting/)
- [Guide to hyperparameter tuning in XGBoost](https://www.analyticsvidhya.com/blog/2016/03/complete-guide-parameter-tuning-xgboost-with-codes-python/)
- [5 SMOTE techniques for oversampling your imbalanced data](https://towardsdatascience.com/5-smote-techniques-for-oversampling-your-imbalance-data-b8155bdbe2b5)
- [How to do cross-validation when upsampling data](https://kiwidamien.github.io/how-to-do-cross-validation-when-upsampling-data.html)
- Which machine learning algorithms require ... ?
	- [feature scaling (standardization and normalization)?](https://www.kaggle.com/getting-started/159643)
	- [one-hot encoding?](https://stats.stackexchange.com/questions/288095/what-algorithms-require-one-hot-encoding)
	- [scaling, besides SVM?](https://stats.stackexchange.com/questions/244507/what-algorithms-need-feature-scaling-beside-from-svm)
- [Shap: shapley additive explanations](https://towardsdatascience.com/a-novel-approach-to-feature-importance-shapley-additive-explanations-d18af30fc21b): feature importance algorithm explained
- [Machine learning operations principles](https://ml-ops.org/content/mlops-principles)
- [The People + AI Guidebook (Google)](https://pair.withgoogle.com/guidebook/): methods, best practices and examples for designing better AI systems


# 📝 formulas/ reminders

Classification metrics:

$\text{Error rate} = \dfrac{FP + FN}{TN + FP + FN + TP}$

$\text{Accuracy} = \dfrac{TP + TN}{TN + FP + FN + TP}$

$\text{Recall} = \text{True positive rate} = \text{Sensitivity} = \dfrac{TP}{TP + FN}$

$\text{Precision} = \text{Positive predicted value} = \dfrac{TP}{TP + FP}$

$\text{F-score} = \text{Harmonic mean of precision and recall} = (1 + \beta^2) \dfrac{Precision \cdot Recall}{(\beta^2 \cdot Precision) + Recall}$

$\text{Specificity} = \text{True negative rate} = \dfrac{TN}{TN + FP}$

$\text{False positive rate} = 1 - \text{Specificity} = \dfrac{FP}{TN + FP}$ 

<br>

Data processing:
> General rule: balancing > scaling > selection

> All models have tendency to overfit to some extent: “If you torture the data long enough, it will confess.” (Nobel Laureate Ronald Coase)


> Logistic regression insights: “All else being equal, if your income had been $20,000 higher you would have been granted this particular mortgage.”
> 
> KNN insigghts: “We declined your mortgage application because you remind us of the Smiths and the Mitchells, who both defaulted.”



# 🌐 machine learning web app
- [Streamlit](https://docs.streamlit.io/): the library to easily create web applications in Python
- [Heroku](https://devcenter.heroku.com/): a library which allows for deployment of your application on the web
- Examples:
	- [Example #1](https://towardsdatascience.com/how-to-build-a-data-science-web-app-in-python-penguin-classifier-2f101ac389f3): building a Penguin classifier deployed on the web
	- [Example #2](https://towardsdatascience.com/how-to-write-web-apps-using-simple-python-for-data-scientists-a227a1a01582): general Streamlit snippets

