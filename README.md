# 🛰️ Network Anomaly Hunter

An interactive machine-learning system for detecting **unusual network behaviour in IoT traffic**.

The goal is simple:

> **Learn what normal network traffic looks like, then identify traffic that behaves differently.**

This project is built to explore anomaly detection as an actual ML problem rather than simply training a classifier and reporting accuracy.

---

## 🎯 Objective

Build an interactive network-monitoring application that:

1. Learns patterns from benign IoT network traffic.
2. Assigns an anomaly score to incoming traffic.
3. Flags unusual traffic for investigation.
4. Provides useful information about why the traffic appears unusual.
5. Visualizes the model's behaviour through an interactive web interface.

The system will **not initially be trained to recognize specific attack types**.

Instead, the model learns:

> **"What does normal traffic look like?"**

Attack labels from the dataset can then be used afterward to evaluate how well the anomaly detector identifies abnormal traffic.

---

## 📊 Dataset

### CIC-IoT2023

The project uses the **CIC-IoT2023 dataset**, developed by the Canadian Institute for Cybersecurity.

The dataset contains network traffic collected from IoT devices and includes benign traffic as well as multiple categories of attacks.

Official dataset:

https://www.unb.ca/cic/datasets/iotdataset-2023.html

The complete dataset is very large, so the project will initially use a manageable subset.

---

## 🧠 Machine Learning Pipeline

```text
CIC-IoT2023
      │
      ▼
Data Cleaning
      │
      ▼
Feature Selection
      │
      ▼
Feature Engineering
      │
      ▼
Scaling / Normalization
      │
      ▼
Train on Benign Traffic
      │
      ▼
Anomaly Detection Model
      │
      ▼
Anomaly Score
      │
      ▼
Threshold
      │
      ├───────────────┐
      ▼               ▼
    Normal         Anomaly
                      │
                      ▼
                Investigation
```

---

## 🤖 Models

The first implementation will experiment with:

* Isolation Forest
* One-Class SVM
* DBSCAN

The models will be compared based on their ability to identify abnormal traffic.

The objective is not simply to find the model with the highest score, but to understand:

* How each algorithm defines "normal"
* How sensitive each model is to anomalies
* False positives
* False negatives
* Threshold selection
* Computational cost

---

## 🔬 Evaluation

Although anomaly detection can be performed without labels, the dataset provides labels that can be used for evaluation.

The project will investigate:

* Precision
* Recall
* F1-score
* Confusion matrix
* False-positive rate
* Detection rate
* Anomaly-score distributions

A major focus will be **false positives**, because a system that labels normal traffic as suspicious too frequently is not very useful in practice.

---

## 🌐 Application Architecture

The project will use:

```text
Vue 3
  │
  │ HTTP / Axios
  ▼
Flask API
  │
  ├── Game / monitoring logic
  ├── Model inference
  └── Analysis
          │
          ▼
      ML Model
          │
          ▼
     Processed Data
```

### Frontend

Vue 3 will provide:

* Network dashboard
* Traffic visualization
* Anomaly alerts
* Anomaly investigation view
* Model statistics

### Backend

Flask will provide APIs for:

* Traffic analysis
* Anomaly detection
* Model statistics
* Individual anomaly investigation

---

## 🚨 Anomaly Investigation

A detected anomaly should not simply appear as:

```text
ANOMALY = TRUE
```

Instead, the application will expose relevant information about the observation.

Example:

```text
🚨 ANOMALY DETECTED

Anomaly Score: 0.93

Protocol: UDP
Packet Rate: High
Packet Size: High
Connection Behaviour: Unusual

Status: SUSPICIOUS
```

The purpose is to make the ML model's output understandable to the user.

---

## 🧪 Experiments

The project will progressively investigate:

### Experiment 1

How well can a model distinguish benign traffic from abnormal traffic?

### Experiment 2

How does feature selection affect anomaly detection?

### Experiment 3

How do different anomaly detection algorithms behave on the same traffic?

### Experiment 4

How does changing the anomaly threshold affect false positives and detection rate?

### Experiment 5

Can the model detect attack traffic without being explicitly trained on attack labels?

### Experiment 6

Can the model's anomaly score be presented in a way that is understandable to a human?

---

## 🛠️ Technology Stack

**Machine Learning**

* Python
* NumPy
* Pandas
* Scikit-learn
* Matplotlib / Plotly

**Backend**

* Flask
* REST API

**Frontend**

* Vue 3
* Axios
* Tailwind CSS

**Dataset**

* CIC-IoT2023

---

## 📁 Planned Structure

```text
network-anomaly-hunter/
│
├── data/
│   └── README.md
│
├── notebooks/
│   ├── exploration.ipynb
│   └── experiments.ipynb
│
├── ml/
│   ├── preprocessing.py
│   ├── features.py
│   ├── train.py
│   ├── detect.py
│   └── evaluate.py
│
├── backend/
│   ├── app.py
│   └── routes/
│
├── frontend/
│   └── vue-app/
│
├── models/
│
├── requirements.txt
│
└── README.md
```

---

## 🚧 Development Roadmap

### Phase 1 — Data

* [ ] Download dataset
* [ ] Inspect features
* [ ] Understand labels
* [ ] Select manageable subset
* [ ] Clean data

### Phase 2 — ML

* [ ] Build preprocessing pipeline
* [ ] Train first anomaly detector
* [ ] Generate anomaly scores
* [ ] Select threshold
* [ ] Evaluate results
* [ ] Compare models

### Phase 3 — Backend

* [ ] Create Flask application
* [ ] Load trained model
* [ ] Create prediction endpoint
* [ ] Create statistics endpoint
* [ ] Create anomaly investigation endpoint

### Phase 4 — Frontend

* [ ] Build dashboard
* [ ] Display traffic statistics
* [ ] Display anomaly alerts
* [ ] Create investigation page
* [ ] Visualize anomaly scores

### Phase 5 — Improvement

* [ ] Feature importance / explanation
* [ ] Model comparison
* [ ] Better visualizations
* [ ] Streaming/simulated live traffic
* [ ] Performance optimization

---

## ⚠️ Important Note

This project is an **educational ML experiment** and is not intended to provide production-grade cybersecurity protection.

The purpose is to understand anomaly detection, machine-learning pipelines, model behaviour, and how an ML model can be integrated into an interactive application.

---

## 💡 Why This Project?

Most introductory ML projects follow:

```text
Dataset
   ↓
Train
   ↓
Accuracy
   ↓
Done
```

Network Anomaly Hunter is intended to go further:

```text
Real-world data
      ↓
ML reasoning
      ↓
Anomaly detection
      ↓
Human investigation
      ↓
Interactive system
```

The goal is not just to **train a model**.

The goal is to **build something around the model**.
