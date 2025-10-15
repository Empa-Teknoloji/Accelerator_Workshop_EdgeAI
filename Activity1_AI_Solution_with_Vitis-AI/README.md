<p align="center">
    <img src="../Additionals/Empa-Workshops-Template-Banner.jpg" alt="Accelerator Workshops" 
    style="display: block; margin: 0 auto"/>
</p>

# 1) Developing AI Applications on FPGA Platforms with Vitis-AI

Welcome to the Accelerator Workshops event organized by Empa Electronics.  
This guide will walk you through the development steps for our application "Common Object Detection on the Kria Platform with YOLOv5", which demonstrates end-to-end deployment of a deep learning model on an AMD FPGA platform using open-source machine learning libraries and public model checkpoints.

The activity application is a comprehensive demo that begins from an upstream repository and covers the full workflow for deploying an open-source object detection AI model on FPGA-based platforms using the AMD Vitis-AI toolchain. The model can detect 80 common COCO classes (for example: person, car, dog, cell phone, bottle, laptop) as 2D bounding boxes. The demo aims to present all steps required for compatibility, including model architecture review, architectural modifications, quantization and more.

For this workshop we used the Ultralytics YOLOv5s (small) model as a starting point. Two modifications were necessary for DPU compatibility and were applied: the model head forward pass was adjusted to remove some post-processing steps, and the SiLU activation was replaced with LeakyReLU because SiLU is not supported by Vitis-AI. The modified model architecture was retrained using a small amount of data to obtain a new model checkpoint. As a result, the YOLOv5 model was obtained as a single DPU subgraph.

The modified YOLOv5 model is then quantized to INT8 to create an arithmetically compatible version of the model for the DPU (floating-point arithmetic is limited on the DPU). In subsequent steps the model is compiled for a specific DPU architecture and can be executed on a Kria KV260 Vision AI Starter Kit using the Vitis-AI Runtime GraphRunner API.

## Installation
First, follow the setup steps at the link below to prepare the development environment.
### ↳ [Development Environment Installation](Installation.md)
Contains steps for installing the necessary software and tools for the activity.

## Application
### ↳ [Vitis-AI Development Notebook: Quantize & Compile YoloV5s](./yolov5/Application_Quantize_Compile_YoloV5s_using_Vitis-AI.ipynb)
This notebook contains the development steps executed in the official Vitis-AI Docker container environment for the "Common Object Detection on the Kria Platform with YOLOv5" application.

### ↳ [Model Implementation: Common Object Detection on Kria with YOLOv5](Implementation.md)
Contains test and deployment steps for the activity on the AMD Kria KV260 Starter Kit platform.
