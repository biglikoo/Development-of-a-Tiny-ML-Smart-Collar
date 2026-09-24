# Development of a TinyML Smart Collar for Livestock Health Prediction

Welcome to the repository for my undergraduate thesis engineering project. This repository contains the data processing, feature engineering, and machine learning pipeline for an extreme-edge, TinyML-powered smart collar designed to autonomously predict viral pathogenesis (such as Peste des Petits Ruminants - PPR) in indigenous Yankasa and Ouda sheep.

## 📖 Project Background
In rural pastoralist communities, livestock constitutes a critical economic foundation. However, traditional health monitoring relies on intermittent human observation, which often misses the subclinical febrile and respiratory anomalies that occur during viral incubation. 

To address this diagnostic latency, this project proposes a shift from reactive observation to proactive, data-driven edge computing. We engineered an ESP32-based wearable equipped with a multimodal sensor array (IMU, dermal thermometer, and piezoelectric strain transducer) to continuously track physical and physiological biometrics.

Instead of streaming raw, high-frequency data to the cloud—which rapidly drains batteries and fails in rural areas with poor cellular infrastructure—this system processes the data **locally on the device** using Tiny Machine Learning (TinyML), transmitting only single-byte anomaly flags via NB-IoT.

## 🧠 The Machine Learning Pipeline
The Jupyter Notebook included in this repository (`Smart_Collar_Data_Pipeline_and_Model.ipynb`) documents the complete computational lifecycle:

* **Signal Processing & Feature Engineering:** Formatting raw sensor telemetry into 4-second sliding windows (16 Hz) and applying a mathematical thermoregulatory offset to isolate true endogenous febrile spikes from tropical ambient heat stress.
* **Cost-Sensitive Learning:** Livestock datasets are heavily imbalanced (animals are healthy most of the time). Instead of generating physiologically impossible synthetic data, we trained a **Weighted Random Forest (WRF)** algorithm augmented with a **10:1 cost-sensitive penalty matrix** to strictly prioritize rare, pathogenic minority classes.
* **Extreme-Edge Quantization:** Porting and quantizing the trained ensemble model into an INT8 C++ header file capable of executing on the ESP32 in under one millisecond.

## 📊 Key Results
* **Predictive Fidelity:** The quantized model achieved **96.0% overall accuracy** and a **macro-averaged F1-score of 0.94**.
* **Pathogenic Sensitivity:** The 10:1 penalty matrix successfully enforced a **100% diagnostic recall rate** across all acute pathogenic classes (Feverish, Sluggish, Respiratory Distress), ensuring zero false negatives for critically ill subjects.
* **Hardware Efficiency:** Microcontroller profiling confirmed deterministic, sub-millisecond execution (0.837 ms total pipeline latency), proving that complex physiological inference can be sustained on low-power battery constraints.

## 🚀 About the Author
This project was developed as part of my B.Eng in Electrical and Electronics Engineering at the Federal University of Technology, Minna. I am deeply interested in Embedded Systems, Edge AI (TinyML), and building infrastructure-independent hardware for resource-constrained environments. 

Feel free to explore the code, and reach out if you share an interest in applying machine learning to the physical world!
