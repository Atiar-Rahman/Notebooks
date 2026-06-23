
# Machine Learning Tutorial

Last Updated : 5 Jun, 2026

Machine learning is a branch of Artificial Intelligence that focuses on developing models and algorithms that let computers learn from data without being explicitly programmed for every task. In simple words, ML teaches systems to think and understand like humans by learning from the data.

![introduction_to_machine_learning.webp](https://media.geeksforgeeks.org/wp-content/uploads/20251226163208311310/introduction_to_machine_learning.webp)![introduction_to_machine_learning.webp](https://media.geeksforgeeks.org/wp-content/uploads/20251226163208311310/introduction_to_machine_learning.webp)

  
Machine Learning is mainly divided into three core types:

- [****Supervised Learning****](https://www.geeksforgeeks.org/machine-learning/supervised-machine-learning/)****:**** Trains models on labeled data to predict or classify new, unseen data.
- [****Unsupervised Learning****](https://www.geeksforgeeks.org/machine-learning/unsupervised-learning/): Finds patterns or groups in unlabeled data, like clustering or dimensionality reduction.
- [****Reinforcement Learning****](https://www.geeksforgeeks.org/machine-learning/what-is-reinforcement-learning/): Learns through trial and error to maximize rewards, ideal for decision-making tasks.

> ****Note:**** The following are not part of the original three core types of ML, but they have become increasingly important in real-world applications, especially in deep learning.
> 
> ****Additional Types****:
> 
> - [****Self-Supervised Learning****](https://www.geeksforgeeks.org/machine-learning/self-supervised-learning-ssl/): It is often considered as a subset of unsupervised learning, but it has grown into its own field due to its success in training large-scale models. It generates its own labels from the data, without any manual labeling.
> - [****Semi-Supervised Learning****](https://www.geeksforgeeks.org/machine-learning/ml-semi-supervised-learning/)****:**** This approach combines a small amount of labeled data with a large amount of unlabeled data. It’s useful when labeling data is expensive or time-consuming.

## Module 1: Machine Learning Pipeline

This section covers preprocessing, exploratory data analysis and model evaluation to prepare data, uncover insights and build reliable models.

### 1. Data Preprocessing

- [Introduction](https://www.geeksforgeeks.org/machine-learning/introduction-machine-learning/)
- [ML workflow](https://www.geeksforgeeks.org/machine-learning/machine-learning-lifecycle/)
- [Data Cleaning](https://www.geeksforgeeks.org/data-analysis/data-cleaning-introduction/)
- [Data Preprocessing in Python](https://www.geeksforgeeks.org/data-analysis/data-preprocessing-machine-learning-python/)
- [Feature Scaling](https://www.geeksforgeeks.org/machine-learning/feature-engineering-scaling-normalization-and-standardization/)
- [Feature Extraction](https://www.geeksforgeeks.org/machine-learning/what-is-feature-extraction/)
- [Feature Engineering](https://www.geeksforgeeks.org/machine-learning/what-is-feature-engineering/)
- [Feature Selection Techniques](https://www.geeksforgeeks.org/machine-learning/feature-selection-techniques-in-machine-learning/)

### 2. Exploratory Data Analysis

- [Exploratory Data Analysis](https://www.geeksforgeeks.org/data-analysis/what-is-exploratory-data-analysis/)
- [Exploratory Data Analysis in Python](https://www.geeksforgeeks.org/data-analysis/exploratory-data-analysis-in-python/)
- [Advance EDA](https://www.geeksforgeeks.org/data-analysis/advanced-eda/)
- [Time Series Data Visualization](https://www.geeksforgeeks.org/data-analysis/time-series-data-visualization-in-python/)

### 3. Model Evaluation

- [Regularization in Machine Learning](https://www.geeksforgeeks.org/machine-learning/regularization-in-machine-learning/)
- [Confusion Matrix](https://www.geeksforgeeks.org/machine-learning/confusion-matrix-machine-learning/)
- [Precision, Recall](https://www.geeksforgeeks.org/machine-learning/precision-and-recall-in-machine-learning/) and [F1-Score](https://www.geeksforgeeks.org/machine-learning/f1-score-in-machine-learning/)
- [AUC-ROC Curve](https://www.geeksforgeeks.org/machine-learning/auc-roc-curve/)
- [Cross-validation](https://www.geeksforgeeks.org/machine-learning/cross-validation-machine-learning/)
- [Hyperparameter Tuning](https://www.geeksforgeeks.org/machine-learning/hyperparameter-tuning/)

## Module 2: Supervised Learning

Supervised learning algorithms are generally categorized into ****two main types:**** 

- [****Classification****](https://www.geeksforgeeks.org/machine-learning/getting-started-with-classification/): where the goal is to predict discrete labels or categories 
- [****Regression****](https://www.geeksforgeeks.org/machine-learning/regression-in-machine-learning/): where the aim is to predict continuous numerical values.

![supervised_learning](https://media.geeksforgeeks.org/wp-content/uploads/20251226163331844635/supervised_learning.webp "Click to enlarge")

Supervised Learning

There are many algorithms used in supervised learning each suited to different types of problems. Some of the most commonly used supervised learning algorithms are:

### 1. Linear Regression

This is one of the simplest ways to predict numbers using a straight line. It helps find the relationship between input and output.

- [Introduction to Linear Regression](https://www.geeksforgeeks.org/machine-learning/ml-linear-regression/)
- [Gradient Descent in Linear Regression](https://www.geeksforgeeks.org/machine-learning/gradient-descent-in-linear-regression/)
- [Multiple Linear Regression](https://www.geeksforgeeks.org/machine-learning/ml-multiple-linear-regression-using-python/)

### 2. Logistic Regression

Used when the output is a "yes or no" type answer. It helps in predicting categories like pass/fail or spam/not spam.

- [Understanding Logistic Regression](https://www.geeksforgeeks.org/machine-learning/understanding-logistic-regression/)
- [Cost function in Logistic Regression](https://www.geeksforgeeks.org/machine-learning/ml-cost-function-in-logistic-regression/)

### 3. ****Decision Trees****

A model that makes decisions by asking a series of simple questions, like a flowchart. Easy to understand and use.

- [Decision Tree in Machine Learning](https://www.geeksforgeeks.org/machine-learning/decision-tree-introduction-example/)
- [Types of Decision tree algorithms](https://www.geeksforgeeks.org/machine-learning/decision-tree-algorithms/)
- [Decision Tree - Regression (Implementation)](https://www.geeksforgeeks.org/machine-learning/python-decision-tree-regression-using-sklearn/)
- [Decision tree - Classification (Implementation)](https://www.geeksforgeeks.org/machine-learning/building-and-implementing-decision-tree-classifiers-with-scikit-learn-a-comprehensive-guide/)

### 4. ****Support Vector Machines (SVM)****

A bit more advanced—it tries to draw the best line (or boundary) to separate different categories of data.

- [Understanding SVMs](https://www.geeksforgeeks.org/machine-learning/support-vector-machine-algorithm/)
- [SVM Hyperparameter Tuning - GridSearchCV](https://www.geeksforgeeks.org/machine-learning/svm-hyperparameter-tuning-using-gridsearchcv-ml/)
- [Non-Linear SVM](https://www.geeksforgeeks.org/machine-learning/ml-non-linear-svm/)

### ****5. k-Nearest Neighbors (k-NN)****

This model looks at the closest data points (neighbors) to make predictions. Super simple and based on similarity.

- [Introduction to KNN](https://www.geeksforgeeks.org/machine-learning/k-nearest-neighbours/)
- [Decision Boundaries in K-Nearest Neighbors (KNN)](https://www.geeksforgeeks.org/machine-learning/understanding-decision-boundaries-in-k-nearest-neighbors-knn/)

### 6. Naïve Bayes

A quick and smart way to classify things based on probability. It works well for text and spam detection.

- [Introduction to Naive Bayes](https://www.geeksforgeeks.org/machine-learning/naive-bayes-classifiers/)
- [Gaussian Naive Bayes](https://www.geeksforgeeks.org/machine-learning/gaussian-naive-bayes/)
- [Multinomial Naive Bayes](https://www.geeksforgeeks.org/machine-learning/multinomial-naive-bayes/)
- [Bernoulli Naive Bayes](https://www.geeksforgeeks.org/machine-learning/bernoulli-naive-bayes/)
- [Complement Naive Bayes](https://www.geeksforgeeks.org/machine-learning/complement-naive-bayes-cnb-algorithm/)

### ****7. Random Forest (Bagging Algorithm)****

A powerful model that builds lots of decision trees and combines them for better accuracy and stability.

- [Introduction to Random forest](https://www.geeksforgeeks.org/machine-learning/random-forest-algorithm-in-machine-learning/)
- [Random Forest Classifier](https://www.geeksforgeeks.org/dsa/random-forest-classifier-using-scikit-learn/)
- [Random Forest Regression](https://www.geeksforgeeks.org/machine-learning/random-forest-regression-in-python/)
- [Hyperparameter Tuning in Random Forest](https://www.geeksforgeeks.org/machine-learning/random-forest-hyperparameter-tuning-in-python/)

### 8. Introduction to Ensemble Learning

[Ensemble learning](https://www.geeksforgeeks.org/machine-learning/a-comprehensive-guide-to-ensemble-learning/) combines multiple simple models to create a stronger, smarter model. There are mainly two types of ensemble learning:

- [Bagging](https://www.geeksforgeeks.org/machine-learning/what-is-bagging-classifier/) that combines multiple models trained independently.
- [Boosting](https://www.geeksforgeeks.org/machine-learning/adaboost-in-machine-learning/) that builds models sequentially each correcting the errors of the previous one.

## Module 3: Unsupervised learning

Unsupervised learning are again divided into ****three main categories**** based on their purpose: 

- [Clustering](https://www.geeksforgeeks.org/machine-learning/clustering-in-machine-learning/) 
- [Association Rule Mining](https://www.geeksforgeeks.org/machine-learning/association-rule/)
- [Dimensionality Reduction](https://www.geeksforgeeks.org/machine-learning/dimensionality-reduction/)

![unsupervised_learning](https://media.geeksforgeeks.org/wp-content/uploads/20251226163413465185/unsupervised_learning.webp "Click to enlarge")

Unsupervised learning

### ****1. Clustering****

Clustering algorithms group data points into clusters based on their similarities or differences. Types of clustering algorithms are:

****Centroid-based Methods:****

- [K-Means clustering](https://www.geeksforgeeks.org/machine-learning/k-means-clustering-introduction/)
- [Elbow Method for optimal value of k in KMeans](https://www.geeksforgeeks.org/machine-learning/elbow-method-for-optimal-value-of-k-in-kmeans/)
- [K-Means++ clustering](https://www.geeksforgeeks.org/machine-learning/ml-k-means-algorithm/)
- [K-Mode clustering](https://www.geeksforgeeks.org/machine-learning/k-mode-clustering-in-python/)
- [Fuzzy C-Means (FCM) Clustering](https://www.geeksforgeeks.org/machine-learning/ml-fuzzy-clustering/)

****Distribution-based Methods****:

- [Gaussian mixture models](https://www.geeksforgeeks.org/machine-learning/gaussian-mixture-model/)
- [Expectation-Maximization Algorithm](https://www.geeksforgeeks.org/machine-learning/ml-expectation-maximization-algorithm/)
- [Dirichlet process mixture models (DPMMs)](https://www.geeksforgeeks.org/machine-learning/dirichlet-process-mixture-models-dpmms/)

****Connectivity based methods:****

- [Hierarchical clustering](https://www.geeksforgeeks.org/machine-learning/hierarchical-clustering/)
- [Agglomerative Clustering](https://www.geeksforgeeks.org/machine-learning/implementing-agglomerative-clustering-using-sklearn/)
- [Divisive clustering](https://www.geeksforgeeks.org/artificial-intelligence/divisive-clustering/)
- [Affinity propagation](https://www.geeksforgeeks.org/machine-learning/affinity-propagation/)

****Density Based methods:****

- [DBSCAN (Density-Based Spatial Clustering of Applications with Noise)](https://www.geeksforgeeks.org/machine-learning/dbscan-clustering-in-ml-density-based-clustering/)
- [OPTICS (Ordering Points To Identify the Clustering Structure)](https://www.geeksforgeeks.org/machine-learning/ml-optics-clustering/)

### 2. Dimensionality Reduction

Dimensionality reduction is used to simplify datasets by reducing the number of features while retaining the most important information.

- [Principal Component Analysis (PCA)](https://www.geeksforgeeks.org/data-analysis/principal-component-analysis-pca/)
- [t-distributed Stochastic Neighbor Embedding (t-SNE)](https://www.geeksforgeeks.org/machine-learning/ml-t-distributed-stochastic-neighbor-embedding-t-sne-algorithm/)
- [Non-negative Matrix Factorization (NMF)](https://www.geeksforgeeks.org/machine-learning/non-negative-matrix-factorization/)
- [Independent Component Analysis (ICA)](https://www.geeksforgeeks.org/machine-learning/ml-independent-component-analysis/)
- [Isomap](https://www.geeksforgeeks.org/machine-learning/isomap-a-non-linear-dimensionality-reduction-technique/)
- [Locally Linear Embedding (LLE)](https://www.geeksforgeeks.org/machine-learning/swiss-roll-reduction-with-lle-in-scikit-learn/)

### 3. Association Rule

Find patterns between items in large datasets typically in [market basket analysis](https://www.geeksforgeeks.org/data-science/market-basket-analysis-in-data-mining/).

- [Apriori algorithm](https://www.geeksforgeeks.org/machine-learning/apriori-algorithm/)
- [Implementing apriori algorithm](https://www.geeksforgeeks.org/machine-learning/implementing-apriori-algorithm-in-python/)
- [FP-Growth (Frequent Pattern-Growth)](https://www.geeksforgeeks.org/machine-learning/frequent-pattern-growth-algorithm/)
- [ECLAT (Equivalence Class Clustering and bottom-up Lattice Traversal)](https://www.geeksforgeeks.org/machine-learning/ml-eclat-algorithm/)

## Module 4: Reinforcement Learning

Reinforcement learning interacts with environment and learn from them based on rewards.

![agent](https://media.geeksforgeeks.org/wp-content/uploads/20251226164034650871/agent.webp "Click to enlarge")

Reinforcement Learning

### 1. ****Model-Based Methods****

These methods use a model of the environment to predict outcomes and help the agent plan actions by simulating potential results.

- [Markov decision processes (MDPs)](https://www.geeksforgeeks.org/machine-learning/markov-decision-process/)
- [Bellman equation](https://www.geeksforgeeks.org/machine-learning/bellman-equation/)
- [Value iteration algorithm](https://www.geeksforgeeks.org/python/implement-value-iteration-in-python/)
- [Monte Carlo Tree Search](https://www.geeksforgeeks.org/machine-learning/monte-carlo-tree-search-mcts-in-machine-learning/)

### ****2. Model-Free Methods****

The agent learns directly from experience by interacting with the environment and adjusting its actions based on feedback.

- [Q-Learning](https://www.geeksforgeeks.org/machine-learning/q-learning-in-python/)
- [SARSA](https://www.geeksforgeeks.org/machine-learning/sarsa-reinforcement-learning/)
- [Monte Carlo Methods](https://www.geeksforgeeks.org/python/monte-carlo-integration-in-python/)
- [Reinforce Algorithm](https://www.geeksforgeeks.org/machine-learning/reinforce-algorithm/)
- [Actor-Critic Algorithm](https://www.geeksforgeeks.org/machine-learning/actor-critic-algorithm-in-reinforcement-learning/)
- [Asynchronous Advantage Actor-Critic (A3C)](https://www.geeksforgeeks.org/machine-learning/asynchronous-advantage-actor-critic-a3c-algorithm/)

## Module 5: Semi Supervised Learning

It uses a mix of labeled and unlabeled data making it helpful when labeling data is costly or it is very limited.

![semi_supervised_learning](https://media.geeksforgeeks.org/wp-content/uploads/20260226114833948590/semi_supervised_learning.webp "Click to enlarge")

Semi Supervised Learning

- [Semi Supervised Classification](https://www.geeksforgeeks.org/machine-learning/semi-supervised-classification/)
- [Self-Training in Semi-Supervised Learning](https://www.geeksforgeeks.org/machine-learning/self-training-in-semi-supervised-learning/)
- [Few-shot learning in Machine Learning](https://www.geeksforgeeks.org/machine-learning/few-shot-learning-in-machine-learning/)

## Module 6: Forecasting Models

Forecasting models analyze past data to predict future trends, commonly used for time series problems like sales, demand or stock prices.

- [ARIMA (Auto-Regressive Integrated Moving Average)](https://www.geeksforgeeks.org/machine-learning/model-selection-for-arima/)
- [SARIMA (Seasonal ARIMA)](https://www.geeksforgeeks.org/machine-learning/sarima-seasonal-autoregressive-integrated-moving-average/)
- [Exponential Smoothing (Holt-Winters)](https://www.geeksforgeeks.org/artificial-intelligence/exponential-smoothing-for-time-series-forecasting/)

## Module 7: Deployment of ML Models

The trained ML model must be integrated into an application or service to make its predictions accessible.

- [Machine learning deployment](https://www.geeksforgeeks.org/machine-learning/machine-learning-deployment/)
- [Deploy ML Model using Streamlit Library](https://www.geeksforgeeks.org/machine-learning/deploy-a-machine-learning-model-using-streamlit-library/)
- [Deploy ML web app on Heroku](https://www.geeksforgeeks.org/machine-learning/deploy-your-machine-learning-web-app-streamlit-on-heroku/)
- [Create UIs for prototyping Machine Learning model with Gradio](https://www.geeksforgeeks.org/machine-learning/python-create-uis-for-prototyping-machine-learning-model-with-gradio/)

APIs allow other applications or systems to access the ML model's functionality and integrate them into larger workflows.

- [Deploy Machine Learning Model using Flask](https://www.geeksforgeeks.org/machine-learning/deploy-machine-learning-model-using-flask/)
- [Deploying ML Models as API using FastAPI](https://www.geeksforgeeks.org/machine-learning/deploying-ml-models-as-api-using-fastapi/)

MLOps ensure they are deployed, monitored and maintained efficiently in real-world production systems.

- [MLOps](https://www.geeksforgeeks.org/machine-learning/mlops-everything-you-need-to-know/)
- [Continuous Integration and Continuous Deployment (CI/CD) in MLOps](https://www.geeksforgeeks.org/machine-learning/continuous-integration-and-continuous-deployment-ci-cd-in-mlops/)
- [End-to-End MLOps](https://www.geeksforgeeks.org/machine-learning/end-to-end-mlops-pipeline-a-comprehensive-project/)

> - ****For project ideas refer to:**** [100+ Machine Learning Projects with Source Code [2025]](https://www.geeksforgeeks.org/machine-learning/machine-learning-projects/) for hands-on implementation on projects
> - After machine learning and have hands on experience in it we can start with deep learning from here: [Deep Learning Tutorial](https://www.geeksforgeeks.org/deep-learning/deep-learning-tutorial/)


--------
