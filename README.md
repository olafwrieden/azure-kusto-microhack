# Azure Data Explorer Microhack (Preview)

Kusto Product Group and Microsoft Global Black Belt team are pleased to present this challenge based, collaboration driven, discover-by-doing learning experience to you. Microhacks are divided into three parts to cater enough time for the participants to understand the key concepts of Azure Data Explorer effectively.

- [**Microhack 1: Cluster creation and data ingestion**](https://github.com/Azure/azure-kusto-microhack1)
This MicroHack will focus on enabling the participants to design ADX based big data analytics solution, create an ADX cluster, and ingest data into the cluster.

- [**Microhack 2: Data exploration and visualization using Kusto Query Language (KQL)**](https://github.com/Azure/azure-kusto-microhack2)
This MicroHack will focus on enabling the participants to write Kusto queries to explore and analyze the data stored in the clusters. Participants will also create cool visualizations. It is recommended to complete the Microhack 1 before beginning with Microhack 2.

- [**Microhack 3: Advanced capabilities**](https://github.com/Azure/azure-kusto-microhack3)
This Microhack will focus on enabling the participants to create Materialized Views, Functions, and use advanced operators to explore and analyze the data.

---
Earn a digital badge! In order to receive the ADX microhack digital badge, you will need to complete the challenges marked with 🎓 in each Microack. Please submit the KQL queries/commands using the answer sheets found at the beginning of each microack. </br></br>
<p align="center"><img src="/assets/images/badge.png" width="200"></p>
---



### Scenario 

Contoso is a supply chain logistics company that runs a fleet of ships, trucks, and cargo planes to transport and deliver goods around the world. Some of the world’s largest enterprises rely on Contoso’s logistics capabilities to deliver goods to their end customers. Contoso has invested in connecting its fleet with sensors that measure temperature, pressure, humidity, tilt, shock, and light exposure inside its fleet. These sensors emit telemetry data every 1 minute, property data whenever there is a change in the device property, and command data whenever a new command is executed. 

Contoso is looking for suitable data storage and analytical solution that provides out of the box integration with Azure IoT services such as IoT Hub, Event Hubs as well as can read data from storage accounts. Contoso is developing a SaaS application that will allow its customers to track, trace and monitor their shipments. Contoso wants to offer out of the box visualizations with interactive capabilities to enable its customers to drill-in/drill-out of the data. Contoso will offer its customers to view and analyze the last 6 months data. Contoso will retain every customer’s data for up to 1 year. Contoso wants to offer blazing fast loading of visualizations to its customers.
This MicroHack walks through the steps in designing, creating, and configuring Azure Data Explorer clusters keeping in mind these requirements. Once the cluster is deployed, this MicroHack enlists the steps to ingest data into ADX databases and tables using various integration methods such as One Click ingestion.

### Pre-requisites
- An Azure subscription
- (Not applicable for proctor led events) Deploy IoT Central application, create simulated devices and create Data Exports to Event Hubs and Storage Accounts (use this guide to create this infrastructure). For proctor led events, this infrastructure has been pre-created for you. Proctor will provide connection strings, or SAS tokens at an appropriate stage of the hack.
- Authorization to create an Azure Data Explorer cluster or Synapse Data Explorer Pool

### Overview - The microhack architecture

The following architecture has been deployed for you, except the ADX cluster and its integration with other Azure services.
IoT Central acts as the source of telemetry generated by Contoso’s sensors installed on its fleet of trucks, vessels, and airplanes. Telemetry data is streamed on a continuous basis to the Event Hub. Device logs, device property changes and commands executed on the devices are stored in a Storage Account as blobs. 

![Screen capture 1](/assets/images/architecture_diagram.png)

### Deployment Instructions

You can deploy the aforementioned architecture using the steps mentioned below:

On the [Azure Cloud Shell](https://shell.azure.com/) run the following commands to deploy the solution:

  1. Login to Azure
  ```
  az login
  ```
  
  Note: You must do this step or you will see errors when running the script when connecting to IoT Central

  2. If you have more than one subscription, select the appropriate one:
  ```
  az account set --subscription "<your-subscription>"
  ```

  3. Get the latest version of the repository
  ```
  git clone https://github.com/MSUSSolutionAccelerators/ADX-IoT-Analytics-Solution-Accelerator.git
  ```

  Optionally, you can update the [iotanalyticsLogistics.parameters.json](https://github.com/bwatts64/ADXIoTAnalytics/blob/main/iotanalyticsLogistics.parameters.json) file to   personalize your deployment.

  4. Deploy solution
  ```
  cd ADXIoTAnalytics
  . ./deploy.sh
  ```

  5. Choose option 2 to deploy from the options provided
  

### What is Azure Data Explorer and when is it a good fit?

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
- [**Microhack 1: Cluster creation and data ingestion**](https://github.com/Azure/azure-kusto-microhack1)

- [**Microhack 2: Data exploration and visualization using Kusto Query Language (KQL)**](https://github.com/Azure/azure-kusto-microhack2)

- [**Microhack 3: Advanced capabilities**](https://github.com/Azure/azure-kusto-microhack3)
