# ML Model Management with JFrog Artifactory and JFrog Security Essentials (Xray)

## Overview

Use this notebook to experiment with the JFrog Artifactory MLOps feature and the model scanning capabilities for the Hugging Face model hub. 

This project is a fork of the demo that was originally presented at SwampUp 2023 ([Github repo](https://github.com/jfrog/ml-repo-demo)) and more details can be found on the blog post [JFrog brings DevOps best practices to ML development](https://jfrog.com/blog/jfrog-brings-devops-best-practices-to-ml-development).

The second part of the demo is inspired to the stock prediction work available in [this](https://github.com/Poulinakis-Konstantinos/Stock_prediction_with_News_Sentiment_Analysis) Github repo.

## Demo

The execution flow of the demo is the following:

![Demo preview](img/demo_preview.gif)

* Install PyPI packages via Artifactory
* Read configuration file to setup Hugging Face hub via Artifactory
* Block Hugging Face model because it doesn't have a licence
* Tag frogs in image using another Hugging Face mode that has a licence, hence not blocked by the security policy
* Perform a Sentiment Analys for the desired stock with Hugging Face model:
    * The top negative and positive headlines will be displayed alongside a pie chart and plot distribution of the data
	* A few catchy future headlines will be processed by the transformer to see what would be the market reaction to them
    * This sentiment analysis model doesn't have a licence, but it's allowed because we defined an exception for it

## Pre-requisites

1. **PyPI repo:** create a remote repository on Artifactory for PyPI and use the [Set-Me-Up](https://jfrog.com/help/r/jfrog-artifactory-documentation/pypi-repositories) to get the snippet to configure your local ```~/.pip/pip.conf```.
2. **ML repo:** create a remote repository on Artifactory for the Hugging Face hub and use the [Set-Me-Up](https://jfrog.com/help/r/jfrog-artifactory-documentation/hugging-face-repositories) to get: repository URL, access token, snippet to resolve models. Update the ```config.yml``` file with the URL and token just created.
3. **Policy and watch:** Create a JFrog Security Essentials (Xray) [policy](https://jfrog.com/help/r/jfrog-security-documentation/creating-xray-policies-and-rules) to block unknown licences and a watch [watch](https://jfrog.com/help/r/jfrog-security-documentation/configuring-xray-watches) to enforce it on the newly created remote repository.
4. Define an [ignore rule](https://jfrog.com/help/r/jfrog-security-documentation/ignore-rules) for the model ```ProsusAI/finbert```.
5. Install the latest version of Python: ```brew install python```
6. Download the stock headlines data from [kaggle](https://www.kaggle.com/datasets/miguelaenlle/massive-stock-news-analysis-db-for-nlpbacktests) and extract the content in the ```Financial_News``` folder. Ensure you have the following three files: ```analyst_ratings_processed.csv```, ```raw_analyst_ratings.csv```, ```raw_partner_headlines.csv```.
7. Configure a local Jupyter Lab environemnt to run the ML notebook using one of the following options:
    a. ```brew install jupyterlab```
    b. Run the notebook via VS Code
    c. Use an alternative options or a different ML development environment

## Run

1. Open the ```demo.ipynb``` notebook in your preferred ML development environment
2. Update the ```stock_ticker``` and ```stock_name``` variables in the *Import required packages* cell with the details of the stock ticker and name of the company you want to analyse
3. Run the notebook, both PyPI and Hugging Face packages will be resolved via Artifactory

## Extra : running in a virtual env

