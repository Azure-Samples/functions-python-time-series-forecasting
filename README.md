---
topic: sample
languages:
    - python
products:
    - azure-functions
author: priyaananthasankar
---

# Time Series Forecasting using Autoregression Model

This sample uses functions to forecast temperatures based on a series of temperature data. It uses statsmodel autoregression to retrain the data.

# Getting Started

## Deploy to Azure

### Prerequisites

- Install Python 3.6+
- Install [Functions Core Tools](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local#v2)
- Install Docker
- Note: If run on Windows, use Ubuntu WSL to run deploy script

### Steps

- Click Deploy to Azure Button to deploy resources

[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/)

or

- Deploy through Azure CLI
    - Open AZ CLI and run ```az group create -l [region] -n [resourceGroupName]``` to create a resource group in your Azure subscription (i.e. [region] could be westus2, eastus, etc.)
    - Run ```az group deployment create --name [deploymentName] --resource-group [resourceGroupName] --template-file azuredeploy.json```

- Download dataset from here https://raw.githubusercontent.com/jbrownlee/Datasets/master/daily-min-temperatures.csv

- Deploy Function App
  - [Create/Activate virtual environment](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-python#create-and-activate-a-virtual-environment)
  - Run `func azure functionapp publish [functionAppName] --build-native-deps` 

## Test

- Upload the [csv dataset](https://raw.githubusercontent.com/jbrownlee/Datasets/master/daily-min-temperatures.csv) to the forecastinput container blob either through portal or through following Azure CLI

```
az storage blob upload --container-name forecastinput --account-name {storageName} -f {dataset} -n daily-minimum-temperatures.csv
```

- Send the following body in a HTTP POST request as a query param where
name: Input CSV file
result: Forecast output graph image

```
http://[functionappname]/api/ForecastAPI?name=daily-minimum-temperatures.csv&result=series.png

```

## Local Testing

For any local testing, use the sample local.settings.json and host.json, create [virtual environment](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-python#create-and-activate-a-virtual-environment) and run `func host start`

# References

- [Create your first Python Function](https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-python)
- [Time Series Autoregression Model](https://machinelearningmastery.com/autoregression-models-time-series-forecasting-python/ )