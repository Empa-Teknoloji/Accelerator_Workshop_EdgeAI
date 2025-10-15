<p align="center">
    <img src="../Additionals/Empa-Workshops-Template-Banner.jpg" alt="Accelerator Workshops" 
    style="display: block; margin: 0 auto"/>
</p>

# STM32CubeAI Output Implementation on the MindBoard

First, create a new project for our CubeAI application. In STM32CubeIDE click File -> New -> STM32 Project from an Existing STM32CubeMX Configuration File (.ioc).
<div align="center">
  <img width="100%" height="100%" src="Additionals/CubeAI_Doc1.png">
</div>
<br />
Then, as shown below, select the `AI_Workshop.ioc` file located under `CubeMX_Project_Files` in the downloaded folder, give the project a name, and press Finish.
<div align="center">
  <img width="100%" height="100%" src="Additionals/CubeAI_Doc2.png">
</div>
<br />

From the opened IOC page, click Software Packs -> Select Component. In the window that appears open the `X-CUBE-AI` package and check the `core` option as shown in the image below.

<div align="center">
  <img width="100%" height="100%" src="Additionals/CubeAI_Doc3.PNG">
</div>
<br />

After returning to the IOC configuration page by clicking "Ok", you will see the `X-CUBE-AI` option listed under Middleware and Software Packs. Click this option and ensure the `Artificial Intelligence` mode is selected. In the Configuration section below you will see `Main` and a `+` icon.

Click the `+` icon to create a new network. When using Cube AI you can choose between three model types: TFLite, Keras and ONNX. The prebuilt model provided in the repository is a TFLite model, so select TFLite and add your model (or the provided model) using the Browse button. Check the configuration using the settings shown below.

<div align="center">
  <img width="100%" height="100%" src="Additionals/CubeAI_Doc4.PNG">
</div>
<br />

Before saving the IOC file you must run the model analysis. Click the **Analyze** button in the X-CUBE-AI Configuration section. You should see an analysis result similar to the image below.

<div align="center">
  <img width="100%" height="100%" src="Additionals/CubeAI_Doc5.PNG">
</div>
<br />

After the analysis completes, press CTRL+S to generate code from the IOC file.

Next, open `AI_Workshop/Core/Src/main.c` and add the following includes between the

```c
/* USER CODE BEGIN Includes */

/* USER CODE END Includes */
```

comments:

```c
#include <stdio.h>

#include "ai_platform.h"
#include "network.h"
#include "network_data.h"

#include "ism330is.h"
#include "custom_bus.h"
```

These lines add the libraries we will use to the main file. Then add the following global variables between

```c
/* USER CODE BEGIN PV */

/* USER CODE END PV */
```


```c
ai_handle network;
float aiInData[AI_NETWORK_IN_1_SIZE];
float aiOutData[AI_NETWORK_OUT_1_SIZE];
ai_u8 activations[AI_NETWORK_DATA_ACTIVATIONS_SIZE];
const char* activities[AI_NETWORK_OUT_1_SIZE] = {
  "CIRCLE", "HORIZONTAL", "STANDBY", "TRIANGLE", "VERTICAL"
};
ai_buffer * ai_input;
ai_buffer * ai_output;

ISM330IS_Object_t ism330_obj_o;
ISM330IS_IO_t ism330_ctx;
uint8_t ism330_id;
ISM330IS_Capabilities_t ism330_cap;
ISM330IS_Axes_t ism330_axes;
```

Next, add the prototypes between

```c
/* USER CODE BEGIN PFP */

/* USER CODE END PFP */
```


```c
static void AI_Init(void);
static void AI_Run(float *pIn, float *pOut);
static uint32_t argmax(const float * values, uint32_t len);
uint8_t ism330_sensor_init(void);
```

Then add the definitions of the prototype functions inside

```c
/* USER CODE BEGIN 4 */

/* USER CODE END 4 */
```

First, add the sensor initialization function so we can initialize our sensor:

```c
uint8_t ism330_sensor_init(void) {
	ism330_ctx.BusType = ISM330IS_I2C_BUS;
	ism330_ctx.Address = ISM330IS_I2C_ADD_H;
	ism330_ctx.Init = BSP_I2C1_Init;
	ism330_ctx.DeInit = BSP_I2C1_DeInit;
	ism330_ctx.ReadReg = BSP_I2C1_ReadReg;
	ism330_ctx.WriteReg = BSP_I2C1_WriteReg;
	ism330_ctx.GetTick = BSP_GetTick;

	if (ISM330IS_RegisterBusIO(&ism330_obj_o, &ism330_ctx) != ISM330IS_OK)
		return 1;

	if (ISM330IS_ReadID(&ism330_obj_o, &ism330_id) != ISM330IS_OK)
		return 1;

	if (ism330_id != ISM330IS_ID)
		return 1;

	if (ISM330IS_Init(&ism330_obj_o) != ISM330IS_OK)
		return 1;

	if (ISM330IS_ACC_Enable(&ism330_obj_o) != ISM330IS_OK)
		return 1;

	if (ISM330IS_GYRO_Enable(&ism330_obj_o) != ISM330IS_OK)
		return 1;

	return 0;
}
```

For AI activations and preparing the network, add this init function:

```c
static void AI_Init(void)
{
  ai_error err;

  /* Create a local array with the addresses of the activations buffers */
  const ai_handle act_addr[] = { activations };
  /* Create an instance of the model */
  err = ai_network_create_and_init(&network, act_addr, NULL);
  if (err.type != AI_ERROR_NONE) {
    printf("ai_network_create error - type=%d code=%d\r\n", err.type, err.code);
    Error_Handler();
  }
  ai_input = ai_network_inputs_get(network, NULL);
  ai_output = ai_network_outputs_get(network, NULL);
}
```

After setting up the model inputs, add the Run function to execute the model:

```c
static void AI_Run(float *pIn, float *pOut)
{
  ai_i32 batch;
  ai_error err;

  /* Update IO handlers with the data payload */
  ai_input[0].data = AI_HANDLE_PTR(pIn);
  ai_output[0].data = AI_HANDLE_PTR(pOut);

  batch = ai_network_run(network, ai_input, ai_output);
  if (batch != 1) {
    err = ai_network_get_error(network);
    printf("AI ai_network_run error - type=%d code=%d\r\n", err.type, err.code);
    Error_Handler();
  }
}
```

Finally, add the argmax function to find the index of the highest probability among activations:

```c
static uint32_t argmax(const float * values, uint32_t len)
{
  float max_value = values[0];
  uint32_t max_index = 0;
  for (uint32_t i = 1; i < len; i++) {
    if (values[i] > max_value) {
      max_value = values[i];
      max_index = i;
    }
  }
  return max_index;
}
```

To enable printf over UART, add the following function between

```c
/* USER CODE BEGIN 0 */

/* USER CODE END 0 */
```


```c
int _write(int fd, char * ptr, int len)
{
  HAL_UART_Transmit(&huart1, (uint8_t *) ptr, len, HAL_MAX_DELAY);
  return len;
}
```

To call the init functions in `main`, add the following between

```c
 /* USER CODE BEGIN 2 */

/* USER CODE END 2 */
```


```c
  ism330_sensor_init();
  AI_Init();
```

Before calling `AI_Run`, we need to prepare the model inputs. The prebuilt model expects 768 samples ordered as accX[n], accY[n], accZ[n], gyroX[n], gyroY[n], gyroZ[n]. Therefore, inside the main `while (1)` loop add the following between

```c
 /* USER CODE BEGIN WHILE */

  /* USER CODE END WHILE */
```


```c
  for(uint32_t i = 0; i < AI_NETWORK_IN_1_SIZE; i=i+6)
	  {
		  ISM330IS_ACC_GetAxes(&ism330_obj_o, &ism330_axes);
		  aiInData[i + 0] = ism330_axes.x;
		  aiInData[i + 1] = ism330_axes.y;
		  aiInData[i + 2] = ism330_axes.z;
		  ISM330IS_GYRO_GetAxes(&ism330_obj_o, &ism330_axes);
		  aiInData[i + 3] = ism330_axes.x/100;
		  aiInData[i + 4] = ism330_axes.y/100;
		  aiInData[i + 5] = ism330_axes.z/100;
		  HAL_Delay(8);
	  }
```

This code collects sensor data into `aiInData`. After filling `aiInData`, call the model with:

```c
AI_Run(aiInData, aiOutData);
```

To print the outputs, add the following code:

```c
   /* Output results */
      for (uint32_t i = 0; i < AI_NETWORK_OUT_1_SIZE; i++) {
        printf("%8.6f ", aiOutData[i]);
      }
      uint32_t class = argmax(aiOutData, AI_NETWORK_OUT_1_SIZE);
      printf(": %d - %s\r\n", (int) class, activities[class]);
```

The code is ready — embed it to the board to test.
