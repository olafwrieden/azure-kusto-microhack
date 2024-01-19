# Azure Data Explorer Microhack

## Introduction

Azure Data Explorer Microhack is a challenge-based, collaboration-driven, discover-by-doing learning experience. Microhacks are divided into three modules called "labs" to cater enough time for the participants to understand the key concepts of Azure Data Explorer. As topics activities build on one another, it is recommended to complete the labs in order.

- [**Lab 1:** ADX Cluster Creation, Data Ingestion and Exploration](/Lab1.md)
  This lab focuses on enabling the participants to design ADX based big data analytics solution, create an ADX cluster, and ingest data from a variety of common sources into the cluster.

- [**Lab 2:** Data exploration and visualization using Kusto Query Language (KQL)](/Lab2.md)
  Building on Lab 1, Lab 2 focuses on enabling the participants to write kusto queries to explore and analyze the telemetry data stored in the clusters. This includes anomaly detection, forecasting, and other advanced operations. Participants will also create common visualizations.

- [**Lab 3:** Advanced KQL, Policies, & Security](/Lab3.md)
  This lab will focus on enabling the participants to create Materialized Views, Functions, and use advanced operators including Row-Level Security to prepare data assets for production scenarios.

### Earn a Microsoft badge!

In order to receive the "Azure Data Explorer Microhack" digital badge, you will need to complete the challenges marked with 🎓 in each lab. Please submit the KQL queries/commands using the answer sheets found at the beginning of each lab. You may edit your answers after or try again.

<p align="center"><img src="/assets/images/Badge-microhack-2stars.png" width="300"></p>

Let's get familiar with the scenario below and start micro-hacking!

---

## Scenario

Contoso is a supply chain logistics company that runs a fleet of ships, trucks, and cargo planes to transport and deliver goods around the world. Some of the world’s largest enterprises rely on Contoso’s logistics capabilities to deliver goods to their end customers. Contoso has invested in connecting its fleet with sensors that measure temperature, pressure, humidity, tilt, shock, and light exposure inside its fleet. These sensors emit telemetry data every 1 minute, property data whenever there is a change in the device property, and command data whenever a new command is executed.

Contoso is looking for a suitable data storage and analytical solution that provides out-of-the-box integration with Azure IoT services such as Azure IoT Hub, Azure Event Hubs and can read data from Azure Storage Accounts and Amazon S3 Buckets.

Contoso is developing a SaaS application that will allow its customers to track, trace and monitor their shipments. Contoso wants to offer out-of-the-box visualizations with interactive capabilities to enable its customers to drill-in/drill-out of the data.

Contoso will offer its customers to view and analyze the last 1 month of data and will retain every telemetry data for up to 1 year.

Contoso wants to offer blazing fast loading of visualizations to its customers. Additionally, a team of data scientists at Contoso are required to perform advanced analytics on the data to detect anomalies, forecast trends, and bring in external data sources to enrich the IoT telemetry.

This microhack walks through the steps of designing, creating, and configuring an Azure Data Explorer cluster for this scenario. Once the cluster is deployed, this microhack covers ingesting data into a KQL databases using various integration methods such as One-Click ingestion from common data sources. As your new ADX skills are put to the test, you can refer back to these requirements or think about them as anecdotes for your own business challenges.

_Can you help Contoso get started with Azure Data Explorer?_

## Pre-requisites

- An Azure Subscription
- The deployed solutioon architecture to create simulated device telemetry (steps to create the infrastructure are given below).
- Authorization to create an Azure Data Explorer cluster or Fabric Real-Time Analytics Databases.

## Overview: Microhack Architecture

The following architecture has been deployed for you, except for the ADX cluster and its integration with other Azure services (Azure Event Hub, Azure Storage Account, and external connections to Power BI or external data).

![Screen capture 1](/assets/images/architecture.png)

**Azure Function App**
Acts as the source of telemetry generated by Contoso's sensors installed on its fleet of trucks, vessels, and airplanes. Telemetry data is streamed on a continuous basis to the Azure Event Hub.

**Azure Storage Account**
Contains a selection of historical data that you will import once in Lab 1, and an NYC Taxi Dataset you will use later in the microhack.

**External Tables**
An externally-maintained CSV dataset containing lookup values you will use to enrich data in later labs.

### Deployment Instructions

You can deploy the aforementioned architecture using the steps mentioned below:

On the [Azure Cloud Shell](https://shell.azure.com/), use bash to run the following commands to deploy the solution:

1. Login to Azure

```shell
az login
```

Note: You must do this step and log in using the prompted URL, even if you're already logged in to Azure. Otherwise, you will see errors when running the script when connecting to IoT Central.

2. If you have more than one subscription, select the appropriate one:

```shell
az account set --subscription "<your-subscription-ID>"
```

3. Get the latest version of the repository

```shell
git clone https://github.com/MSUSSolutionAccelerators/ADX-IoT-Analytics-Solution-Accelerator.git
```

Optionally, you can update the cloned [iotanalyticsLogistics.parameters.json](https://github.com/MSUSSolutionAccelerators/ADX-IoT-Analytics-Solution-Accelerator/blob/main/iotanalyticsStore.parameters.json) file to personalize your deployment.

4. Deploy solution

```shell
cd ADX-IoT-Analytics-Solution-Accelerator
. ./deploy.sh
```

5. Choose option 2 to deploy from the options provided

6. This is the expected result: <img src="/assets/images/Deployment_Check_CLI_Screenshot.png" width="1370">

> **Tip** 📝 Write down the name of the Resource Group that has been created (indicated in green in the image above).

### Confirm Deployment Success (optional)

After the deployment is complete, do the following checks to confirm data is flowing into Event Hub.

1. Open the Resource Group that is created newly and check that one Event Hub, one IoT Central Application and one Storage Account are created.
2. Open IoT Central Application, and from overview page, click on the IoT Central Application URI.
3. A new web page with Azure IoT Central will open. From the "Devices" menu, check 30 test devices are created and simulated.
   ![IoT Central Devices simulation](/assets/images/Deployment_Check1_pic1.png)
4. Similarly, from the "Data export" tab on the left hand menu, check that both Export and Destination are healthy.
   ![IoT Central Destination Check](/assets/images/Deployment_Check2_pic1.png)
   ![IoT Central Export Check](/assets/images/Deployment_Check2_pic2.png)

5. Now from the Azure Portal, open the Event Hub that was created, and check the graph "Messages" in the overview page. Note that the simulated devices messages should be flowing into the Event Hub and the number of messages should not be zero.
   <img src="/assets/images/Deployment_Check_EH_messages.png" width="540">

**Note:** Data from Event Hub is crucial for successfully setting up ingestion into ADX. Please take help from the proctor if messages are not flowing into the Event Hub.

---

## What is Azure Data Explorer and when is it a good fit?

Azure Data Explorer is a fully managed, high-performance, big data analytics platform that makes it easy to analyze high volumes of data in near real time. The Azure Data Explorer toolbox gives you an end-to-end solution for data ingestion, query, visualization, and management.

By analyzing structured, semi-structured, and unstructured data across time series, and by using Machine Learning, Azure Data Explorer makes it simple to extract key insights, spot patterns and trends, and create forecasting models. Azure Data Explorer is scalable, secure, robust, and enterprise-ready, and is useful for log analytics, time series analytics, IoT, and general-purpose exploratory analytics.

Azure Data Explorer capabilities are extended by other services built on its powerful query language, including [Azure Monitor logs](https://docs.microsoft.com/en-us/azure/log-analytics/), [Application Insights](https://docs.microsoft.com/en-us/azure/application-insights/), [Time Series Insights](https://docs.microsoft.com/en-us/azure/time-series-insights/), and [Microsoft Defender for Endpoint](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint)

### How to start with ADX

Generally, when starting with Azure Data Explorer, you will follow the following steps (ADX Microhacks will cover all these steps):

1. **Create an ADX cluster**: To use Azure Data Explorer you first create a cluster. An Azure Data Explorer cluster is the most basic unit.
2. **Create database**: Each cluster has one or more databases in that cluster. Each Azure Data Explorer cluster can hold up to 10,000 databases and each database up to 10,000 tables.
3. **Ingest data**: Load data into database tables so that you can run queries against it. Azure Data Explorer supports several ingestion methods.
4. **Query data**: Azure Data Explorer uses the Kusto Query Language, which is an expressive, intuitive, and highly productive query language. It offers a smooth transition from simple one-liners to complex data processing scripts, and supports querying structured, semi-structured, and unstructured (text search) data. Use the web application to run, review, and share queries and results. You can also send queries programmatically (using an SDK) or to a REST API endpoint.
5. **Visualize results**: Use different visual displays of your data in the native Azure Data Explorer Dashboards. You can also display your results using connectors to some of the leading visualization services, such as Power BI and Grafana.

### Ready to go? It's Microhack time!

- [**Lab 1:** ADX Cluster Creation, Data Ingestion and Exploration](/Lab1.md) 👈 Begin here!
- [**Lab 2:** Data exploration and visualization using Kusto Query Language (KQL)](/Lab2.md)
- [**Lab 3:** Advanced KQL, Policies, & Security](/Lab3.md)
