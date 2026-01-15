# Prometheus Monitoring Stack on AWS

## 📌 Project Overview

This project demonstrates a **real-world end-to-end monitoring solution** using **Prometheus** to monitor multiple layers of a cloud-based system deployed on **AWS EC2**.

The monitoring stack covers:

* Infrastructure (Node-level metrics)
* Containers (Docker metrics)
* Application (Python Flask custom metrics)
* Database (MySQL metrics)

Prometheus is deployed on a **dedicated EC2 instance** and scrapes metrics remotely from other EC2 nodes, simulating a production-like monitoring architecture.

---

## 🏗️ Architecture Overview

### EC2 Instances

1️⃣ **Prometheus Server EC2**

* Runs Prometheus
* Responsible for scraping and storing metrics

2️⃣ **Application Node EC2**

* Docker Engine
* Node Exporter (OS metrics)
* cAdvisor (Container metrics)
* Dockerized Python Flask Application

3️⃣ **Database Node EC2 **

* MySQL Server
* MySQL Exporter

📊 **Metrics Flow**

```
Application / Exporters  --->  Prometheus Server
        (Pull Model)
```

---

## 🧰 Tech Stack

* **Prometheus** – Metrics collection & storage
* **Node Exporter** – OS-level metrics (CPU, memory, disk)
* **cAdvisor** – Container-level metrics
* **MySQL Exporter** – Database monitoring
* **Python (Flask)** – Application exposing custom metrics
* **Docker** – Application containerization
* **AWS EC2** – Cloud infrastructure

---

## 📁 Project Structure

```
monitoring-prometheus-project/
│
├─ app/
│   ├─ app.py               # Flask application
│   ├─ Dockerfile           # Container build file (Image)
│
├─ prometheus/
│   └─ prometheus.yml       # Prometheus scrape configuration
│
│
└─ README.md
```

---

## 🐍 Python Flask Application

The Flask application exposes:

* `/metrics` endpoint (Prometheus-compatible metrics)
Note: The application must import and use the Prometheus client library inside the Flask app to define and expose metrics.
### Custom Metric Example

* `http_requests_total`

  * Counts total HTTP requests received by the application

The application runs inside a Docker container and exposes metrics using the `prometheus_client` library.

---

## 🐳 Dockerization

The Flask application is containerized using Docker:

* Lightweight Python base image
* Exposes port `5000`
* Runs the application on `0.0.0.0` to allow external scraping

This allows Prometheus to scrape metrics directly from the container via the host EC2 private IP.

---

## 📡 Prometheus Configuration

Prometheus uses **static_configs** for simplicity.
The configuration includes the following scrape jobs:

* **Prometheus self-monitoring**
* **Node Exporter** – OS metrics
* **cAdvisor** – Container metrics
* **Python Flask Application** – Custom app metrics
* **MySQL Exporter** – Database metrics

> IP addresses in the repository are replaced with placeholders.

---

## 📊 Metrics Covered

### Infrastructure Metrics (Node Exporter)

* CPU usage
* Memory usage
* Disk I/O
* Load average

### Container Metrics (cAdvisor)

* CPU usage per container
* Memory usage per container
* Network I/O

### Application Metrics (Flask)

* Total HTTP requests
* Request rate

### Database Metrics (MySQL Exporter)

* Connection count
* Query performance
* Buffer pool usage


## 🚀 Why This Project Matters

This project demonstrates:

* Understanding of Prometheus **pull-based monitoring model**
* Real-world **multi-node monitoring architecture**
* Clear separation between monitoring and application workloads
* Monitoring across **infrastructure, containers, and applications**
* Cloud deployment best practices using AWS

## 👨‍💻 Author

**Yousof Khaled**


