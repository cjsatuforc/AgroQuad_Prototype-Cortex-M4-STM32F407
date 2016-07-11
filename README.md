# AgroQuad_Prototype-Cortex-M4-STM32F407

# Hardware
The schematics and Layout of the Flight Control Board can be found here: https://drive.google.com/open?id=0B2tfhqDjs2sUbGIwY3VqNENHMXc

<b>Modules used:</b>
<ul>
	<li>MPU6050 - Accelerometer and Gyroscope</li>
	<li>HMC5883L - Magnetometer</li>
  <li>HC-SR04 - Ultrasonic Sensor (For Collision Avoidance)</li>
  <li>uBlox 6M - GPS</li>
  <li>XBee S2 - Wireless Communication (ZigBee)</li></ul>

# System Description
<p>The Modules are interfaced with the flight control board and a wireless communication is set up using two XBees. The Quadcopter is controlled using a Ground Control Station based on Windows or Android. The source code includes the custom protocol used for communication with the Ground Control Station. However, for tests, a simple terminal application had been used. </p>
<p>The <b>Status Paramters</b> (Roll, Pitch and Yaw) of the System are obtained using the Acceleromter, Gyroscope and Magnetometer (MPU6050 and HMC5883L). A <b>Kalman Filter for State Estimation</b> had been designed for the Quadcopter used specifically for this project. For general purposes, a <b>Complementary Filter</b> is used. The source code also includes a Complex Complementary Filter. This had been tested to account for vibrations generated in the system. It's use, however, is not encouraged unless the user has well understood the Design of the Complex Complementary Filter. </p>
<p>The Status Parameters are used as an Input to the <b>PID Control Loop</b>. A fine tuning of the PID Gains is required in order to achieve a stable flight. The Control Parameters (Output of the PID Loop) are the changes in Motor Speeds given in Microseconds. 4 PWM Signals are used as inputs to ESCs which in turn control the Motor Speeds.</p> A complex PID Loop was also designed. However, a highly precise tuning is necessary for its use.</p>
<p>The Process of Measuring the Status Paramters along with obtaining the Output Signals is done in a periodic loop of 4ms.</p>
