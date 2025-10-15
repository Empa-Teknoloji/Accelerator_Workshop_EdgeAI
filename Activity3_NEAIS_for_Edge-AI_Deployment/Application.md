<p align="center">
    <img src="../Additionals/Empa-Workshops-Template-Banner.jpg" alt="Accelerator Workshops" 
    style="display: block; margin: 0 auto"/>
</p>

# 3) Developing Edge-AI Solutions with NanoEdge AI Studio

Welcome to the Edge AI step of the Accelerator Workshops series organized by Empa Electronics.  
This guide will walk you through the development steps for our "Hand Character Recognition" application created with NanoEdge AI Studio.

## 0. What is NanoEdge AI Studio?
NanoEdge AI Studio (NEAIS) is an automated machine learning platform built for embedded systems engineers. It enables users without deep AI expertise to create Edge-AI algorithms and use them free of charge for STMicroelectronics products.

## 1. Preprocessing Workflows

NanoEdge AI Studio is primarily designed for sensor applications that use time-series data. Therefore, users must provide input data formatted appropriately for time-series models.

Appropriate input is achieved by grouping the collected data using a sampling size that matches the intended application.

![Untitled](./Additionals/NEAIS-Preprocesses/Untitled0.png)

For the Human Activity Recognition application used in this workshop, we assume the hand gestures occur within 1 second. When collecting one sample for the model we therefore:
- Insert an 8 ms delay between sensor readings.
- When grouping 128 readings, each sample covers 128 * 8 = 1024 ms which is appropriate for this application.

### 1.1. Data Logger (DL)

- The Data Logger creates a ready-to-use .bin file for data collection with the following configuration options:
    - Supported MCU list,
    - Selected MCU sensors,
    - MCU-specific parameters (per-axis sample size, sample rate, data range, axis count, etc.).
- The generated .bin file can be flashed directly to the target board (use STM32CubeProgrammer for flashing).

![Untitled](./Additionals/NEAIS-Preprocesses/Untitled1.png)

![Untitled](./Additionals/NEAIS-Preprocesses/Untitled2.png)

### 1.2. Data Manipulation (DM)

- After applying selected operations on given datasets, Data Manipulation exports processed data files.
    - Remove rows,
    - Remove columns,
    - Reorder columns (e.g., sampling),
    - Shuffle rows.

![Untitled](./Additionals/NEAIS-Preprocesses/Untitled3.png)

### 1.3. Sampling Finder (SF)

- For continuously collected data, Sampling Finder aims to keep the highest score while finding the smallest possible sampling size and sampling duration.
- Inputs:
    - Classification files,
    - Number of axes used,
    - Sampling frequency,
    - Minimum frequency to test.

![Untitled](./Additionals/NEAIS-Preprocesses/Untitled4.png)

### 1.4. Feature Importance (FI)

- Feature Importance identifies the minimal set of features (columns) that sufficiently separate classes and recommends removing the rest to speed up the model.
- Input: class-specific signal files (not yet converted to time-series windows).


## 2. Models

### 2.1. Detect Anomalies (AD)
(formerly Anomaly Detection)
- Detects anomalies in data.
- Uses a dynamic model.
- Dynamic models can adapt to different boards or conditions by retraining on-device; NEAIS provides an unsupervised, adaptive model that learns on the target MCU.

![Untitled](./Additionals/NEAIS-Models/Untitled0.png)

### 2.2. Detect Outliers (O)
(formerly 1-Class Classification)
- Detects anomalies in data.
- Uses a static model.
- NEAIS provides a pre-trained outlier detection model that produces results on the target MCU.

![Untitled](./Additionals/NEAIS-Models/Untitled1.png)

### 2.3. Classify (C)
(formerly n-Class Classification)
- Classifies n different labels.
- Uses a static model.
- NEAIS provides a pre-trained classification model for the target MCU.

![Untitled](./Additionals/NEAIS-Models/Untitled2.png)

### 2.4. Extrapolate (E)
(formerly Extrapolation)
- Predicts a continuous target value instead of discrete class labels.
- Uses a static model.
- Expects labeled datasets; does not accept USB live inputs.
- NEAIS provides a pre-trained regression model for the target MCU.

![Untitled](./Additionals/NEAIS-Models/Untitled3.png)


## 3. End-to-End Development Steps

For this application we classify 5 hand gestures and expect the model to predict the class names. The appropriate NEAIS application type is **n-Class Classification**.

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled0.jpg)

NEAIS provides tips through almost every step of the workflow. Following these tips can significantly improve model performance.

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled2.png)

### 3.1. Project Settings

- The target boards used in the activity are STM32U5 series MCUs. Select the correct MCU series under "Your Target" as the model will be embedded on these devices.
- Each measurement uses 6 axes; select Sensor Type: Generic and Number of Axes: 6.
- Maximum RAM and Flash usage for the model can be constrained.

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled1.jpg)

Configuration details:

- Target Sensor Model
    - Choose the sensor model to target for embedding the AI library.
- Sensor Type
    - Accelerometer (1-3 axes), Microphone (1 axis), Hall sensor (1-3 axes), Generic, Multisensor.
- Number of Axes / Variables
    - IMPORTANT: NEAIS computes the number of samples from columns divided by the number of axes. (Example: 3-axis accelerometer + 3-axis gyroscope with 128 samples results in 128 * 6 = 768 columns per row.)
- Maximum RAM & Flash constraints for the library.


### 3.2. Signals

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled3.png)

- From File
    - Select separate data files for each class.

    ![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled4.jpg)

    - After selecting files the datasets are previewed. If data is unsuitable, NEAIS highlights problem areas and asks the user to fix them.

- Serial Port (USB)
    - Collect data directly from the USB serial port.

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled5.png)

After importing data:

- Axes correspond to instantaneous measurements in the data columns.
- If data is valid, NEAIS applies a Fast Fourier Transform so signals can be viewed in the Frequency Domain.

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled6.jpg)

- Users can apply a Filter to remove undesired frequency components and limit signals to a specific frequency window.

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled7.png)

### 3.3. Benchmark (Model Training & Performance)

In this section select the classes (signals) and the number of CPU cores to run the benchmark. Each selected dataset is treated as one class.

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled8.jpg)

Click start to run the benchmark; it will begin in a few seconds.

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled9.jpg)

The benchmark screen shows:
- status,
- progress and timestamps,
- performance metrics,
- log window (benchmark status, search speed per core, found libraries, etc.),
- performance evolution over time,
- pause and stop controls.

After the benchmark users can choose one of the trained libraries depending on performance trade-offs.

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled10.jpg)

### 3.4. Validation

Users can compare models using test data and pick a preferred model.

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled11.jpg)

### 3.5. Emulator

The Emulator allows running the model inside NanoEdge AI Studio.

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled12.png)

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled13.png)

### 3.6. Deployment - Obtaining the Model Library

- Users can save the trained model library and example C code by clicking "Compile Library".
- The code samples on the right side guide usage of the model on the target MCU.

![Untitled](./Additionals/NEAIS-End-to-endDeploymentSteps/Untitled14.jpg)
