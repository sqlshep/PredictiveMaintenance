# PredictiveMaintenance

This repo is an update to the original one published here

[Deep Learning for Predictive Maintenance](https://github.com/Azure-Samples/MachineLearningSamples-DeepLearningforPredictiveMaintenance)

The updates to the notebooks include integration with MLFlow and AML Python SDK v2. The data set is from the [NASA CMAPSS Jet Engine Simulated Data](https://data.nasa.gov/Aerospace/CMAPSS-Jet-Engine-Simulated-Data/ff5v-kuh6/data)

# Introduction

Deep learning is one of the most popular trends in the machine learning space with applications to many areas including driverless cars, speech and image recognition, robotics and finance. Deep learning, also referred to as Artificial Neural Networks (ANN), is a set of algorithms inspired by the shape of our brain (biological neural networks).

Predictive maintenance is uses machine learning methods to determine the condition of an equipment in order to preemptively trigger a maintenance visit to avoid adverse machine performance. In these scenarios, data is collected over time to monitor the state of an equipment with the final goal of finding patterns to predict failures. [Long Short Term Memory (LSTM)](http://colah.github.io/posts/2015-08-Understanding-LSTMs/) networks are especially appealing to the predictive maintenance domain due to their ability at learning from sequences of data. LSTM are designed for application to time series data in order to look back over periods of time to detect temporal patterns that could lead to machine failures.

In this scenario, we build a LSTM network for the data set and scenario described at [Predictive Maintenance](https://gallery.azure.ai/Collection/Predictive-Maintenance-Template-3) to predict remaining useful life of aircraft engines. In summary, the template uses simulated aircraft sensor values to predict when an aircraft engine will fail in the future so that maintenance can be planned in advance.

This tutorial uses [keras](https://keras.io/) deep learning library with [Tensorflow](https://www.tensorflow.org/) as the back end.

# Prerequisites

- An [Azure account](https://azure.microsoft.com/en-us/free/) (free trials are available).
- An Azure Machine learning Workspace.
- Azure Machine Learning Compute Instance, CPU or GPU will work, however the LSTM NN will create about 30%-40% on a GPU instance.

# Let's Begin

These notebooks were tested in a Jupyter Notebook on a compute instance within Azure Machine Learning Studio, while these notebooks may work in your own environment, you may have trouble with package dependencies.

Open the Azure Portal in your favorite browser, Navigate to the your Azure Machine Learning workspace and Launch Studio. From there navigate to compute, select your compute instance, then select Jupyter from Applications, this will open an instnace of the Jupyter Browser.

Under **New** in the upper right had corner of the Jupyter Browser select **Terminal**.

Navigate to the location you would like to clone the github repo, then run **git clone** of this repo.

Return to the Jupyter Browser and navigate to teh location you cloned the repo.

# Task 1: Data Ingestion & Preparation

Select the The Data Ingestion Jupyter Notebook in the `LSTM/1_data_ingestion_and_preparation.ipnyb` loads the three input data sets into pandas dataframe format, prepares the data for the modelling and does some preliminary data visualization. The data sets are persisted to a local directory for use in the model building and evaluation task. Make sure you select the **Python 3.8 - Pytorch and Tensorflow** Kernel or newer.

# Task 2: Model Building & Evaluation

The Model Building Jupyter Notebook in `LSTM/2_model_building_and_evaluation_deploy.ipnyb` reads the persisted training and test data sets from local storage and builds a LSTM network. The LSTM model is built using the training data set with two layers plus dropout to prevent overfitting. The model performance is measured on the test set. The resulting model is serialized and stored in the local compute context for use in the operationalization task. MLFlow has been integrated into this note book so you can monitor the progress of the runs in the Azure ML Studio under Jobs.

The operationalization takes the stored model and builds required functions and schema for calling the model on an Azure hosted web service. THe notebook includes the code to register the model and deploy it as an Online Endpoint.
