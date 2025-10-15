<p align="center">
    <img src="../Additionals/Empa-Workshops-Template-Banner.jpg" alt="Accelerator Workshops" 
    style="display: block; margin: 0 auto"/>
</p>

# 2) Developing Edge-AI Solutions on ST Platforms

## Development Environment Setup
### Cloud Development Environment (Development Only)
The cloud environment provided for this activity does not require local installation for development. Note that testing the developed solution requires a local environment with serial port access and cannot be performed in the cloud environment. You can follow the development steps interactively using the Colab notebook linked below.

**1- Colab Notebook Example (Tensorflow with CNN)**  
[Accelerators Workshop - Edge AI - Activity-2 Cloud Development Environment (Tensorflow with CNN)](https://colab.research.google.com/drive/1hXrLQyYdJ7H2DgL7fW6nQtDmb_dmDuge)

**2- Colab Notebook Example (scikit-learn with Random Forests)**
[Accelerators Workshop - Edge AI - Activity-2 Cloud Development Environment (scikit-learn with Random Forests)](https://colab.research.google.com/drive/1bbg1bfcpoIIn0kcI18elS_EtdG5Iee-f)

### Local Development Environment (Testing Only)

## 1- STM32CubeIDE Installation

STM32CubeIDE is an Eclipse-based C/C++ development platform for STM32 microcontrollers and microprocessors. It supports project configuration, code generation and compilation, debugging, and flashing to devices.

First, download STM32CubeIDE 1.17.0 (latest at the time of writing) from here: [https://www.st.com/en/development-tools/stm32cubeide.html#get-software](https://www.st.com/en/development-tools/stm32cubeide.html#get-software)
Choose and install the package that matches your operating system. Note that you must accept the license agreement and create a MyST account and sign in to download the files.
<br />
<div align="center">
  <img width="100%" height="100%" src="Additionals/kurulum1.png">
</div>
<br />

NOTE 1: Make sure the installation path does not contain Turkish characters or spaces.

NOTE 2: During installation you will be asked whether to install ST-LINK and SEGGER J-Link drivers — select them and continue.

## 2- STM32CubeProgrammer Installation

STM32CubeProgrammer is a graphical tool for programming and configuring STM32 microcontrollers.

Download STM32CubeProgrammer 2.18.0 (latest) from here: [https://www.st.com/en/development-tools/stm32cubeprog.html#get-software](https://www.st.com/en/development-tools/stm32cubeprog.html#get-software)
Select and install the version for your operating system. You must accept the license agreement and be signed in to your MyST account to download.

<br />
<div align="center">
  <img width="100%" height="100%" src="Additionals/cubeprogrammer.png">
</div>
<br />

## 3- Tera Term Installation

Tera Term is used to open a serial terminal to the development board (UART). Download the installer from the project's GitHub Releases page: https://github.com/TeraTermProject/teraterm/releases and install the program.
<br />
<div align="center">
  <img width="100%" height="100%" src="Additionals/teraterm.png">
</div>
<br />

## 4- Installing Software Packages

First, sign in to your MyST account for package installation. In STM32CubeIDE select Help -> STM32Cube updates -> Connection to myST.
<div align="center">
  <img width="100%" height="100%" src="Additionals/myst_login.png">
</div>

<br />
Click "Enter myST account information" in the dialog that appears:
<div align="center">
  <img width="100%" height="100%" src="Additionals/myst_connection.png">
</div>
<br />
And sign in to your account:
<div align="center">
  <img width="100%" height="100%" src="Additionals/login.png">
</div>
<br />

# 4-A) Installing the U5 Package

The application uses an STM32U5-series microcontroller, so you must install the U5 MCU package. Start STM32CubeIDE.

In STM32CubeIDE go to Help -> Configuration Tools -> Manage Embedded Software Packages.
<div align="center">
  <img width="100%" height="100%" src="Additionals/manage_embedded_software_packages.png">
</div>

<br />
Under STM32Cube MCU Packages select STM32U5 -> "STM32Cube MCU Package for STM32U5 Series" and check version 1.7.0 (latest). Click Install to download and install the package.
<div align="center">
  <img width="100%" height="100%" src="Additionals/u5_install.png">
</div>
<br />

# 4-B) Installing the X-CUBE-ISPU Software Package

In STM32CubeIDE go to Help -> Configuration Tools -> Manage Embedded Software Packages.
<br />
<div align="center">
  <img width="100%" height="100%" src="Additionals/manage_embedded_software_packages.png">
</div>
<br />

Select STMicroelectronics from the vendor list, then choose the X-CUBE-ISPU package and check the latest version (2.1.0 at the time of writing). Click Install. You must be signed in and accept the license agreement during installation. The package will be downloaded and installed.

<br />
<div align="center">
  <img width="100%" height="100%" src="Additionals/ispu_install.png">
</div>
<br />

# 4-C) Installing the X-CUBE-AI Software Package

In STM32CubeIDE go to Help -> Configuration Tools -> Manage Embedded Software Packages.
<br />
<div align="center">
  <img width="100%" height="100%" src="Additionals/manage_embedded_software_packages.png">
</div>
<br />

Select STMicroelectronics from the vendor list, then choose the X-CUBE-AI package and check version 10.0.0 (latest). Click Install and accept the license agreement when prompted. The package will be downloaded and installed.

<br />
<div align="center">
  <img width="100%" height="100%" src="Additionals/cubeai_package.png">
</div>
<br />

All required installations are complete.
