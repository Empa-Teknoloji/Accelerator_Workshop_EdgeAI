<p align="center">
    <img src="./Additionals/Empa-Workshops-Template-Banner.jpg" alt="Accelerator Workshops" 
    style="display: block; margin: 0 auto"/>
</p>


## Welcome to the Accelerator Workshops!

**Hello!**
This open-source repository is provided by Empa Electronics for participants of our Accelerator Workshops. It contains materials and setup instructions so you can follow along with the workshop activities and experiment afterwards.

**Edge AI**  
The deployment and operation of AI solutions can commonly be done in two different ways. One approach is cloud-based AI, where a model runs on a cloud server (for example AWS/Azure) and incoming data is sent to that model for inference. The other approach is edge AI, where a model runs locally on an edge device (for example a sensor board) and inference results are available directly on that device. Edge AI solutions bring several benefits, such as lower latency, reduced bandwidth usage, lower power consumption, and improved data privacy because data does not need to be sent to another platform for inference.

## Live Demo
No setup is required to attend the live demo presentation in our Edge AI workshop. Demo source files are shared here for review and for use as reference material after the event.

### ↳ [1) Developing AI Applications on FPGA Platforms with Vitis-AI](Activity1_AI_Solution_with_Vitis-AI)
**This activity covers using AI solutions on AMD FPGA platforms with Vitis-AI.** It is presented by the speaker and will not be interactive. The provided materials are intended for post-event experimentation.

## Workshop Activities
For each workshop activity we provide setup instructions and environment materials. Follow the installation guides in each activity folder to prepare your workspace.

### ↳ [2) Developing Edge-AI Solutions for ST MCU Platforms](Activity2_Bare-Metal_Edge-AI_Solution)
This activity focuses on Tiny-ML-style edge AI solutions for STMicroelectronics platforms and includes hands-on exercises. It will be run interactively with participant involvement.

### ↳ [3) Developing Edge-AI Solutions with NanoEdge AI Studio](Activity3_NEAIS_for_Edge-AI_Deployment)
This activity demonstrates how to develop Tiny-ML applications using NanoEdge AI Studio and will be interactive.

## Directory Structure
Each top-level folder contains the materials and setup guides for a specific workshop activity:

```
Workshop Repository
├── Activity1_AI_Solution_with_Vitis-AI
│   ├── Source code & materials
│   └── README.md (Activity-1 Guide)
├── Activity2_Bare-Metal_Edge-AI_Solution
│   ├── Source code & materials
│   └── README.md (Activity-2 Guide)  
└── Activity3_NEAIS_for_Edge-AI_Deployment
    ├── Source code & materials
    └── README.md (Activity-3 Guide) 
```

## Prerequisites - Checklist
Use the checklists below to verify your environment after completing the setup steps for each activity.

Activity-1 (For post-event experimentation)
- [ ] Python 3.8
- [ ] Docker
- [ ] Vitis-AI Docker container environment
- [ ] Activity-1 source files

Activity-2
- [ ] Colab notebook example (no setup required)
- [ ] STM32CubeIDE (STM32CubeMX & STM32CubeAI)
- [ ] STM32CubeProgrammer
- [ ] Activity-2 source files

Activity-3
- [ ] NanoEdge AI Studio
- [ ] STM32CubeIDE (STM32CubeMX)
- [ ] STM32CubeProgrammer
- [ ] Activity-3 source files

## Updates
Keep an eye on this section for updates to the workshop materials and environment.

```
Version-1: 12 February 2025
Initial release: basic guides for all activities were added to the repository.
```

## Notices
If you have questions about the workshop setup or materials, please contact **ai@empa.com**.

To update your local copy of the workshop materials to the latest changes, open a terminal in the Workshop repository folder and run:

```bash
cd Workshop_Workspace/Accelerator-Workshops-EdgeAI
git pull origin master
```
