machine learning core 3 types 
- **supervised learning:** Trains models on labeled data to predict or classify new, unseen data.
- **unsupervised learning:** Finds patterns or groups in unlabeled data, like clustering or `dimensionality` reduction.
- **reinforcement learning:** Learns through trial and error to maximize rewards, ideal for decision-making tasks.

## Module 1: Machine Learning Pipeline

In order to make predictions there are some steps through which data passes in order to produce a machine learning model that can make predictions.

1. [ML workflow](https://www.geeksforgeeks.org/machine-learning/machine-learning-lifecycle/)
2. [Data Cleaning](https://www.geeksforgeeks.org/data-analysis/data-cleansing-introduction/)
3. [Feature Scaling](https://www.geeksforgeeks.org/machine-learning/ml-feature-scaling-part-2/)
4. [Data Preprocessing in Python](https://www.geeksforgeeks.org/machine-learning/data-preprocessing-machine-learning-python/)

## Module 2: Supervised Learning

Supervised learning algorithms are generally categorized into ****two main types:**** 

- [****Classification****](https://www.geeksforgeeks.org/machine-learning/getting-started-with-classification/) - where the goal is to predict discrete labels or categories 
- [****Regression****](https://www.geeksforgeeks.org/machine-learning/regression-in-machine-learning/) - where the aim is to predict continuous numerical values.
### 1. Linear Regression

This is one of the simplest ways to predict numbers using a straight line. It helps find the relationship between input and output.

- [Introduction to Linear Regression](https://www.geeksforgeeks.org/machine-learning/ml-linear-regression/)
- [Gradient Descent in Linear Regression](https://www.geeksforgeeks.org/machine-learning/gradient-descent-in-linear-regression/)
- [Multiple Linear Regression](https://www.geeksforgeeks.org/machine-learning/ml-multiple-linear-regression-using-python/)
- [Ridge Regression](https://www.geeksforgeeks.org/machine-learning/what-is-ridge-regression/)
- [Lasso regression](https://www.geeksforgeeks.org/machine-learning/what-is-lasso-regression/)
- [Elastic net Regression](https://www.geeksforgeeks.org/machine-learning/implementation-of-elastic-net-regression-from-scratch/)

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

### Introduction to Ensemble Learning

[****Ensemble learning****](https://www.geeksforgeeks.org/machine-learning/a-comprehensive-guide-to-ensemble-learning/) combines multiple simple models to create a stronger, smarter model. There are mainly two types of ensemble learning:

- [****Bagging****](https://www.geeksforgeeks.org/machine-learning/What-is-Bagging-classifier/) that combines multiple models trained independently.
- [****Boosting****](https://www.geeksforgeeks.org/machine-learning/boosting-in-machine-learning-boosting-and-adaboost/) that builds models sequentially each correcting the errors of the previous one.



## Module 3: Unsupervised learning

Unsupervised learning are again divided into ****three main categories**** based on their purpose: 

- [Clustering](https://www.geeksforgeeks.org/machine-learning/clustering-in-machine-learning/) 
- [Association Rule Mining](https://www.geeksforgeeks.org/machine-learning/association-rule/)
- [Dimensionality Reduction](https://www.geeksforgeeks.org/machine-learning/dimensionality-reduction/).

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
- [Divisive clustering](https://www.geeksforgeeks.org/machine-learning/difference-between-agglomerative-clustering-and-divisive-clustering/)
- [Affinity propagation](https://www.geeksforgeeks.org/machine-learning/affinity-propagation-in-ml-to-find-the-number-of-clusters/)

****Density Based methods:****

- [DBSCAN (Density-Based Spatial Clustering of Applications with Noise)](https://www.geeksforgeeks.org/machine-learning/dbscan-clustering-in-ml-density-based-clustering/)
- [OPTICS (Ordering Points To Identify the Clustering Structure)](https://www.geeksforgeeks.org/machine-learning/ml-optics-clustering-explanation/)

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

### 1. ****Model-Based Methods****

These methods use a model of the environment to predict outcomes and help the agent plan actions by simulating potential results.

- [Markov decision processes (MDPs)](https://www.geeksforgeeks.org/machine-learning/markov-decision-process/)
- [Bellman equation](https://www.geeksforgeeks.org/machine-learning/bellman-equation/)
- [Value iteration algorithm](https://www.geeksforgeeks.org/python/implement-value-iteration-in-python/)
- [Monte Carlo Tree Search](https://www.geeksforgeeks.org/machine-learning/ml-monte-carlo-tree-search-mcts/)

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


- [Semi Supervised Classification](https://www.geeksforgeeks.org/machine-learning/semi-supervised-classification-in-data-mining/)
- [Self-Training in Semi-Supervised Learning](https://www.geeksforgeeks.org/machine-learning/self-training-in-semi-supervised-learning/)
- [Few-shot learning in Machine Learning](https://www.geeksforgeeks.org/machine-learning/few-shot-learning-in-machine-learning/)

## Module 6: Deployment of ML Models

The trained ML model must be integrated into an application or service to make its predictions accessible.

- [Machine learning deployement](https://www.geeksforgeeks.org/machine-learning/machine-learning-deployment/)
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
