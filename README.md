# Azure Weather Report
This project is a data engineering system that captures, processes, and analyzes weather conditions from anywhere in the world in real time. The end result is an interactive dashboard (for analysis) and an automatic alert system (via email) that warns of important weather events, such as storms or sudden temperature spikes.

## 1. What does it do? (features)

This project implements a complete data pipeline with the following capabilities:

* **Data Ingestion:** Connects to a Weather API to retrieve live data.
* **Data Streaming:** Processes data as it arrives, without the need to wait for batches.
* **Transform & Store:** Enriches and stores data in a database optimized for time series analysis (data that changes over time).
* **Visualization (Reporting):** Displays weather data in a dynamic dashboard in Power BI.
* **Alerts:** Uses Microsoft Fabric Data Activator to monitor data and send alerts (e.g., "Alert: Temperature in São Paulo above 35°C").
* **Governance:** Includes security mechanisms for API keys (Key Vault) and cost monitoring (Cost Management).

## 2. What is this project?

This is not a web or mobile application. This is an end-to-end (E2E) data pipeline and analytics platform.

The code in this repository builds the infrastructure "backbone" and processing logic that makes the alerting system and dashboard possible.

## 3. Core stack

This project uses a modern architecture focused on Azure PaaS (Platform as a Service) services, with a special emphasis on the new **Microsoft Fabric** suite.

| **Category**                  | **Service/Technology**              | **Purpose in Project**                                                                     |
| ----------------------------- | ----------------------------------- | ------------------------------------------------------------------------------------------ |
| **Data Source**               | WeatherAPI (Free Tier)              | Provides real-time weather data.                                                           |
| **Ingestion & Orchestration** | Azure Functions or Azure Databricks (trade-off) | Logic to connect, pull data from the API, and send it to the Event Hub. |
| **Streaming (Queue)**         | Azure Event Hubs                    | Receives ingested data and acts as a high-performance _buffer_ for streaming.              |
| **Central Platform**          | **Microsoft Fabric**                | The unified platform where processing, storage, and analysis occur.                        |
| **Processing (Fabric)**       | EventStream                         | Captures the stream from the Event Hub, transforms, and routes data in real-time.          |
| **Storage (Fabric)**          | EventHouse (KustoDB)                | Database optimized for _large volume_ and time-series analysis (streaming data).           |
| **Analysis (Fabric)**         | Kusto Query Language (KQL)          | Query language used to analyze the data in KustoDB.                                        |
| **Reporting (Delivery)**      | Power BI                            | Creates the live visualization dashboard connected to KustoDB.                             |
| **Alerting (Delivery)**       | Data Activator (Fabric)             | Monitors data in KustoDB and triggers actions (like sending emails).                       |
| **Governance & Ops**          | Azure Key Vault & Cost Management   | Ensure credential security and budget compliance.                                          |

## 4. Project Ambition

The ambition of this project goes beyond "just testing a technology." The goal is to build a **reference architecture** for ingesting and analyzing *any* streaming data at scale.

It is designed to demonstrate proficiency in modern data architecture (Real-Time Intelligence with Fabric) and in making engineering decisions (trade-offs), creating a robust solution that could be easily adapted to an enterprise environment (e.g., monitoring financial transactions, IoT logs, or social media engagement).

## 5. Current Project Status (WIP)

The project is **In Progress**.

| Feature | Status |
| :--- | :--- |

| S01: Research & Setup | 33% |
| :--- | :--- |
| E2E Architecture Definition | ✅ Completed |
| Azure Key Vault and Cost Management Setup | 📄 Pending |
| Event Hub Setup | 📄 Pending |

| S02: Ingestion | 0% |
| :--- | :--- |
| _[WIP]_ *Producer* Development (Azure Function/Databricks) | 🚧 In Progress |
| Testing the connection and sending data from WeatherAPI to Event Hub | 📄 Pending |

| S03: Processing (Fabric) | 0% |
| :--- | :--- |
| Microsoft Fabric (EventStream) Configuration | 📄 Pending |
| EventStream Pipeline for EventHouse (KustoDB) | 📄 Pending |

| S04: Results | 0% |
| :--- | :--- |
| KQL query development (Kusto) | 📄 Pending |
| Dashboard creation in Power BI | 📄 Pending |
| Alert configuration in Data Activator | 📄 Pending |

## 6. Challenges and Known Issues

### **Trade-off:**
* The project intentionally explores **two forms** of ingestion (Azure Functions vs. Databricks).
* **Azure Functions:** It is an excellent *serverless* solution for lightweight, event-based ingestion (triggers), with an excellent cost-benefit ratio for this task.
* **Databricks:** It is more robust, ideal if future ingestion requires complex transformations *before* sending to Event Hub (Spark Streaming).
* *Current Decision:* -

### **API Costs:**
* The project uses the **Free Tier** of WeatherAPI. This imposes a *rate limit* (call limit per minute) that is, at the moment, more than sufficient for this project's showcase. * *Solution:* The architecture is decoupled. Switching to a paid API tier would not require any changes to the rest of the pipeline (from Event Hub onward), demonstrating the scalability of the design.

## 7. Case Study

This project follows a structured data analysis methodology:

1. **Research:** Analysis of available weather APIs and new Microsoft Fabric (Real-Time Intelligence) services.
2. **Data & Conditions:** Defining which data is critical (temperature, precipitation, wind) and which conditions should trigger alerts.
3. **Method:** Designing the E2E architecture (as seen above), focusing on managed services (PaaS) to reduce operational overhead.
4. **Examination (In-Depth Analyzing):** The core of the project. The data will be stored in KustoDB, enabling complex time series analysis using KQL to identify patterns that a traditional database would not.
5. **Result:** The final deliverable: an automated system that provides *insights* (via Power BI) and *actions* (via Data Activator).
