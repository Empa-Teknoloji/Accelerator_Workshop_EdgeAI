<p align="center">
    <img src="../Additionals/Empa-Workshops-Template-Banner.jpg" alt="Accelerator Workshops" 
    style="display: block; margin: 0 auto"/>
</p>

# 1) Developing AI Applications on FPGA Platforms with Vitis-AI

Apply the listed steps in order to deploy the application produced in this activity to the target platform.

## Implementation of the Application

**1- Target Platform Setup**  
Follow the steps on the official AMD Vitis-AI documentation's "Target Installation" page to obtain and prepare the target platform with the required files.

Source: [https://xilinx.github.io/Vitis-AI/3.0/html/docs/quickstart/mpsoc.html#setup-the-target](https://xilinx.github.io/Vitis-AI/3.0/html/docs/quickstart/mpsoc.html#setup-the-target)

**2- Transferring the Application Source Files to the Target Platform**  
Copy the `Scripts` folder provided in the activity materials and the compiled model (the "model compiled" directory) to an appropriate location on the target platform and run the application using Python.

Obtain the local IP address required for SSH on the target by running `ifconfig` on the target's terminal (look for `inet: 192.168...`).

```bash
[target] $ ifconfig
```

Then, from your host machine open an SSH terminal to the target using the address you found (replace the `xxx` with the correct values for your network):

```bash
[host] $ ssh root@192.168.xxx.xxx
```

On the target platform terminal, create a directory to store the application files:

```bash
[target] $ mkdir Vitis-AI && cd Vitis-AI
```

From the host terminal, go into the activity folder (`Activity1_AI_Solution_with_Vitis-AI`) and copy the `Scripts` folder to the target using `scp`:

```bash
[host] $ scp -r Scripts root@192.168.xxx.xxx:/home/root/Vitis-AI/
```

**3- Running the Application on the Target Platform**  
On the Kria KV260 platform running PetaLinux, the preinstalled Python interpreter and the Vitis-AI Runtime library are used to run the application.

Before running, edit the source files in the `Scripts` folder that begin with the `app_` prefix and update any variables that start with `path_` so they point to the correct location of the model files. Then run the application with the Python interpreter:

```bash
[target] $ python3 app_yolov5_video.py
```
