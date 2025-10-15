<p align="center">
    <img src="../Additionals/Empa-Workshops-Template-Banner.jpg" alt="Accelerator Workshops" 
    style="display: block; margin: 0 auto"/>
</p>

# 2) Developing Edge-AI Solutions on ST Platforms

Welcome to the Accelerator Workshops event organized by Empa Electronics.  
This guide will walk you through the development steps for our "Hand Character Recognition" application, which will be implemented using modern machine learning libraries and common workflows.

The activity's "Hand Character Recognition" demo is implemented on the custom Mind Board designed and produced by Empa Electronics. Six-axis sensor measurements from the board's accelerometer and gyroscope are used as input to an AI model running on the edge device to classify five different hand characters. An illustration of the hand characters and how the Mind Board is held is provided below.

<img src="./Additionals/Hand-Characters.png" alt="Hand Characters" width="800"/>

## Installation
First, follow the setup steps at the link below to prepare the development environment.
### ↳ [Development Environment Installation](Installation.md)
Contains installation steps for required software and tools for the activity.

## Application
### ↳ [Hand Character Recognition (TensorFlow CNN)](https://colab.research.google.com/drive/1hXrLQyYdJ7H2DgL7fW6nQtDmb_dmDuge)
This notebook contains development steps for the Hand Character Recognition demo using a CNN built with TensorFlow on Google Colab.

### ↳ [Hand Character Recognition (scikit-learn Random Forest)](https://colab.research.google.com/drive/1bbg1bfcpoIIn0kcI18elS_EtdG5Iee-f)
This notebook contains development steps for the Hand Character Recognition demo using a Random Forest implemented with scikit-learn on Google Colab.

### ↳ [Model Testing (Local): Hand Character Classification](Application_test_local_hand_character_recognition_EN.ipynb)
Local test steps for the Hand Character Recognition application.

### ↳ [STM32CubeAI Output Implementation on the MindBoard](Edgedevice_Project_Installation.md)
Implementation steps for deploying the Hand Character Recognition model on the Mind Board.

### ↳ [Model Testing (Edge): Hand Character Classification](Application_test_edge_hand_character_recognition_EN.ipynb)
Edge-device test steps for the Hand Character Recognition application.

## Edge-AI on ST Platforms

**Training Models with TensorFlow**  
TensorFlow (and its Keras API) is one of the leading open-source frameworks for building deep learning models. Because of its ease of use and high-level API, TensorFlow was chosen as the base framework for the deep learning model developed in this workshop.

**Deploying Edge-AI Solutions with STM32Cube.AI**  
Deploying a trained ML/DL model on ST platforms can be done using the STM32Cube.AI conversion tool provided by STMicroelectronics. STM32Cube.AI supports many popular model formats and includes built-in model compression/compilation tools to help port models to embedded devices.

**References & Further Reading**

1- [TensorFlow 2 Quickstart for Beginners](https://www.tensorflow.org/tutorials/quickstart/beginner)

2- [STM32Cube.AI - A Free Tool For Edge-AI Developers](https://stm32ai.st.com/stm32-cube-ai/)
