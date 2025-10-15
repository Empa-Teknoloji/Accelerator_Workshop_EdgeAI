<p align="center">
    <img src="../Additionals/Empa-Workshops-Template-Banner.jpg" alt="Accelerator Workshops" 
    style="display: block; margin: 0 auto"/>
</p>

# 3) Developing Edge-AI Solutions with NanoEdge AI Studio

Welcome to the Edge AI step of the Accelerator Workshops series organized by Empa Electronics.  
This guide covers installation and development steps for our "Hand Character Recognition" application built with NanoEdge AI Studio.

## Installation
First, follow the setup steps at the link below to prepare the development environment.
### ↳ [NanoEdge AI Studio Installation Guide](Installation.md)
Contains the installation steps for NanoEdge AI Studio and related tools.

## Application
### ↳ [NEAIS Edge-AI: Hand Character Classification](Application.md)
Contains the development steps for the edge AI application in this activity.

## NanoEdge AI Studio
**1- What is NEAIS?**
- **Helps embedded systems engineers** find the ideal AI model for their needs with minimal AI expertise.
- Originally developed by **Cartesiam** (now part of ST) for MCUs running embedded C code.

**2- How does it work?**
- **Runs locally on a PC**,
- **Imports input data**,
- Explores thousands of preprocessing, model and parameter combinations,
- Outputs a **library** (model, preprocessing steps and functions) ready for embedding.

**3- What it doesn't provide**
- Does not provide input data; users must have **qualified data**.
- Does not provide the final ready-to-run **C code** for the project (note: it provides example code snippets and libraries).
- Primarily designed for **sensor applications**.

**4- Features**
- **No deep ML expertise** required.
- **Efficient use of MCU memory**.
- **Optimized for running on MCUs**.

**5- Typical Steps**
- Configure project settings
- Import signals
- **Run benchmark**
- Find and compare libraries (models)
- **Test libraries**
- **Embed on MCU**

**6- Benchmark steps**
- Signal **preprocessing**
- Explore **ML models**
- Optimum **hyperparameter** search

**7- Preprocessing tools**
- **Data Logger (DL)**
- **Data Manipulation (DM)**
- **Sampling Finder (SF)**
- **Feature Importance (FI)**

**8- Model types**
- **Detect Anomalies (AD)**
    - For adaptive, unsupervised anomaly detection that can learn on-device.
- **Detect Outliers (O)**
    - Static model for outlier detection.
- **Classify (C)**
    - Static model for n-class classification.
- **Extrapolate (E)**
    - Regression model for continuous target prediction.

**References & Further Reading**

1- [Wiki by STMicroelectronics - NanoEdge AI Studio](https://wiki.stmicroelectronics.cn/stm32mcu/wiki/AI:NanoEdge_AI_Studio)
