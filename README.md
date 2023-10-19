# PredictiveMaintenance

This repo is an update to the original one published here

[Deep Learning for Predictive Maintenance](https://github.com/Azure-Samples/MachineLearningSamples-DeepLearningforPredictiveMaintenance)

The updates to the notebooks include integration with MLFlow and AML Python SDK v2. The data set is from the [NASA CMAPSS Jet Engine Simulated Data](https://data.nasa.gov/Aerospace/CMAPSS-Jet-Engine-Simulated-Data/ff5v-kuh6/data)

# Introduction

Deep learning is one of the most popular trends in the machine learning space, with application in to many areas including driverless cars, speech and image recognition, robotics and finance. Deep learning, also referred to as Artificial Neural Networks (ANN), is a set of algorithms inspired by the shape of our brain (biological neural networks).

Predictive maintenance uses machine learning methods to determine the condition of equipment in order to preemptively trigger a maintenance visit to avoid adverse machine performance. In these scenarios, data is collected over time to monitor the state of equipment with the final goal of finding patterns to predict failures. [Long Short-Term Memory (LSTM)](http://colah.github.io/posts/2015-08-Understanding-LSTMs/) networks are especially appealing to the predictive maintenance domain due to their ability to learn from sequences of data. LSTMs are designed for application to time series data in order to look back over periods of time to detect temporal patterns that could lead to machine failures.

In this scenario, we build an LSTM network for the dataset and scenario described in [Predictive Maintenance](https://gallery.azure.ai/Collection/Predictive-Maintenance-Template-3) to predict remaining useful life of aircraft engines. In summary, the template uses simulated aircraft sensor values to predict when an aircraft engine will fail in the future so that maintenance can be planned in advance.

This tutorial uses [Keras](https://keras.io/) deep learning library with [TensorFlow](https://www.tensorflow.org/) as the back end.

# Team Data Science Process

![Team Data Science Process lifecycle.](img/tdsp-lifecycle2.png "Team Data Science Process lifecycle.")

The Team Data Science Process (TDSP) is an agile, iterative data science methodology designed to deliver predictive analytics solutions and intelligent applications efficiently. TDSP helps improve team collaboration and learning by suggesting how team roles work best together. TDSP includes best practices and structures from Microsoft and other industry leaders to help toward successful implementation of data science initiatives. The goal is to help companies fully realize the benefits of their analytics program. [Learn More Here](https://learn.microsoft.com/en-us/azure/architecture/data-science-process/overview)

# Prerequisites

- An [Azure account](https://azure.microsoft.com/en-us/free/) (free trials are available).
- An Azure Machine Learning workspace.
- Azure Machine Learning Compute Instance, CPU or GPU will work, however the LSTM NN will create about 30%-40% faster on a GPU instance.

# Let's Begin

These notebooks were tested in a Jupyter Notebook on a compute instance within Azure Machine Learning Studio, while these notebooks may work in your own environment, you may have trouble with package dependencies.

Open the Azure Portal in your favorite browser, Navigate to your Azure Machine Learning workspace and Launch Studio. From there navigate to compute, select your compute instance, then select Jupyter from Applications, this will open an instance of the Jupyter Browser.

Under **New** in the upper right hand corner of the Jupyter Browser select **Terminal**.

Navigate to the location you would like to clone the github repo, then run **git clone** of this repo.

Return to the Jupyter Browser and navigate to the location where you cloned the repo.

# Task 1: Data Ingestion & Preparation

Select the 'The Data Ingestion' Jupyter Notebook in the `LSTM/1_data_ingestion_and_preparation.ipnyb` loads the three input data sets into pandas dataframe format, prepares the data for the modeling and does some preliminary data visualization. The data sets are persisted to a local directory for use in the model building and evaluation task. Make sure you select the **Python 3.8 - Pytorch and Tensorflow** Kernel or newer.

# Task 2: Model Building & Evaluation & Deploy

The Model Building Jupyter Notebook in `LSTM/2_model_building_and_evaluation_deploy.ipnyb` reads the persisted training and test data sets from local storage and builds a LSTM network. The LSTM model is built using the training data set with two layers plus dropout to prevent overfitting. The model performance is measured on the test set. The resulting model is serialized and stored in the local compute context for use in the operationalization task. MLFlow has been integrated into this notebook so you can monitor the progress of the runs in the Azure ML Studio under Jobs.

The operationalization takes the stored model and builds required functions and schema for calling the model on an Azure hosted web service. The notebook includes the code to register the model and deploy it as an Online Endpoint.

# Task 3: Responsible AI

Responsible Artificial Intelligence (Responsible AI) is an approach to developing, assessing, and deploying AI systems in a safe, trustworthy, and ethical way. AI systems are the product of many decisions made by those who develop and deploy them. From system purpose to how people interact with AI systems, Responsible AI can help proactively guide these decisions toward more beneficial and equitable outcomes. That means keeping people and their goals at the center of system design decisions and respecting enduring values like fairness, reliability, and transparency.

[Learn More Here](https://learn.microsoft.com/en-us/azure/machine-learning/concept-responsible-ai?view=azureml-api-2)
