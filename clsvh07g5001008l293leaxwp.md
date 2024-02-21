---
title: "Prometheus"
datePublished: Wed Feb 21 2024 07:26:06 GMT+0000 (Coordinated Universal Time)
cuid: clsvh07g5001008l293leaxwp
slug: prometheus
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708500040931/75474044-f192-445e-b326-f4c3a26d6a4d.png
tags: devops, prometheus, 90daysofdevops

---

### **Prometheus**

This is an open-source system for monitoring services and alerts based on a time series data model. Prometheus collects data and metrics from different services and stores them according to a unique identifier—the metric name—and a time stamp.

Prometheus is designed for reliability, to be the system you go to during an outage to allow you to quickly diagnose problems. It is also designed to monitor highly dynamic container environments.

### **What is the Architecture of Prometheus Monitoring?**

The architecture of Prometheus Monitoring consists of several key components that work together to collect, store, and query metrics. Here are some of the main architectural elements:

1. **The Prometheus server,** Constituting the core of the Prometheus monitoring system, fulfils three primary functions: data collection, data storage, and data processing. Through scraping configured targets at specified intervals, it actively retrieves metrics data (pull-based model). This data is then stored within its internal time-series database for later retrieval and analysis.
    
2. **Exporters** are essential tools in the Prometheus ecosystem, converting metrics from their native formats to Prometheus-compatible formats. These auxiliary processes enable Prometheus to monitor a wide variety of systems and services that do not natively support Prometheus metrics.
    
3. **Targets**: Targets are the endpoints or services that Prometheus queries for metrics, often via HTTP(S). They include applications using Prometheus libraries, exporters for translating metrics, and services with built-in Prometheus support.
    
4. **Alertmanager**: The Alertmanager component oversees the processing of alerts triggered by the Prometheus server, efficiently handling tasks such as merging similar alerts, organizing them into groups, and directing them to the right recipients.
    
5. **Pushgateway:** The Push Gateway is an intermediary service which allows jobs that cannot be scraped (e.g., batch jobs that do not expose an HTTP endpoint) to push metrics to Prometheus. It is an optional component used to support specific use cases where the pull model is not feasible.
    
6. **Client Libraries**: Prometheus's client libraries empower developers to embed code instrumentation directly into their applications, enabling the exposure of diverse metrics to Prometheus for collection. This facilitates comprehensive monitoring, offering support for various metric types across multiple programming languages.
    

### What are the Features of Prometheus?

* **Time-series:** Metrics are stored with timestamps, capturing historical trends and changes over time. 
    
* **PromQL:** This powerful query language lets you analyze, aggregate, and manipulate data to extract meaningful insights.
    
* **Integrations:** Prometheus integrates with tools like Grafana for visualizations and other monitoring platforms, with native support for Kubernetes environments.
    
* **Alertmanager:** A dedicated service handles notification routing and deduplication, ensuring you receive timely and relevant alerts.
    
* **Service Discovery:** Prometheus simplifies target management in dynamic infrastructures through its support for service discovery across environments like Kubernetes and AWS.
    
*  **Pull-Based Metrics Collection:** Prometheus employs a pull-based strategy to gather metrics from various targets. 
    

### What database is used by Prometheus?

Prometheus uses its custom-built time series database (TSDB) for storing metrics data. This TSDB is specifically designed to efficiently handle time series data generated by monitored systems and services. It's optimized for high write and read throughput, efficient storage, and fast queries, making it well-suited for real-time monitoring and analysis tasks.

### What is the default data retention period in Prometheus?

The default data retention period in Prometheus is 15 days. Prometheus retains the collected metrics data for 15 days by default in its time series database before automatically deleting it from the storage. However, the administrator can adjust this retention period based on the specific needs and requirements of the monitoring environment.

Thank you for reading.