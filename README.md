# LoR_Core_SerialControl
Contains the configurations for controlling a MiniBot via serial interface.

Board: ESP32 dev module

This is an Arduino code designed to control a 4-wheel drive robot using an ESP32 development module. The motor controls are configured in a "standard tank style". Serial commands are used to manipulate the robot's movements. This code can be uploaded to a LoR_Core module and paired with a CAMRON module to complete the CAMRON MiniBot system.

The major sections of the code can be summarized as follows:

1. **Library and Definitions:** The code starts by importing the Adafruit_NeoPixel library which is used for controlling LED lights on the robot. It then defines a number of constants and variables related to the robot's configuration. These include settings for version control, IO interfaces, motor pin definitions, PWM configurations, NeoPixel configurations, and motor speed limits. 

2. **Setup Function:** In the setup function, all motor and LED pins are initialized. LED PWM functionalities are configured, and the serial communication is established for debugging purposes and for secondary communication with other devices, such as the Camron module.

3. **Main Loop:** The main loop checks for serial input. If a serial control command is received, the robot LED color is set to green. If no command is received, the robot enters a standby state and the LED color is set to red.

4. **Supporting Functions:** The script has several helper functions for managing the robot's movement and LED display. These include:

   - `NeoPixel_SetColour()`: This function sets the color of all NeoPixel LEDs on the robot.
   - `Set_Motor_Output()`: This function controls the motor output based on received input values.
   - `SlewRateFunction()`: This function manages the slew rate for motor speed ramping, providing a smoother transition between different speed levels.
   - `SerialControl()`: This function handles serial control input and adjusts the motor targets based on the received commands ("Forward", "Backward", "Left", "Right", "Stop").
   - `Motor_Contol()`: This function calls the `Set_Motor_Output()` function for each wheel of the robot, setting the motor speeds to the values determined by the serial control.
   - `Motor_STOP()`: This function stops the motors using the `SlewRateFunction()`.
  
The code also includes several debug print statements for monitoring the robot's state and actions. It uses both serial and secondary serial communication (Serial2) for command inputs and debugging. LED indications are used to denote the control state (Serial - Green LED, none/Stop/standby - Red LED).
