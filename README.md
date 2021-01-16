# SortingMachine
A Color Based Object Sorting Machine that uses a camera running on a Raspberry Pi to take pictures of objects being placed into a detecting area then feeding those pictures into a Deep Learning Model for prediction. After predicting an object, a robotic arm that is being controlled by an Arduino takes the object and sort it in its predicted position.

The main idea behind Colour Based Object Sorting Machine is to identify and sort objects of different shapes and colours by using an image recognition technique developed on a microcontroller in my case (deep learning model running on a Raspberry Pie) as well as a sorting mechanism, also controlled by a microcontroller and here I used (a robotic arm controlled by Arduino). Sorting objects based on their colour is a very helpful technique in many areas, one simple example would be distinguishing good fruits from bad ones and putting them in their respective boxes.  
This project was started as a team if two students. Me as a computer science student who’s responsible for the software part of the project, that is recognising the shape and the colour of the object and determining it position as (x, y) relative to the space it was recognised at using python running on the Raspberry Pie and its requirements in the design as well as connecting the Raspberry Pie to the Arduino which is controlling the robotic arm.  And my teammate as computer engineer student who’s responsible for controlling the robotic arm to pick an object from (x1, y1) position and place them in (x2, y2) position using inverse kinematics. 
For my teammate private reasons, he couldn’t continue to work on the project which lead me to do some modification to the design where I can reach the same results without needing to control the arm to pick objects from (x, y) position using inverse kinematics and instead it will move to and from predefined positions.  

1.Hardware components. 
2.The code for taking the pictures and processing them.
3.A convolutional neural network model for predicting objects and their color. 
4.Using the model to tell the robotic arm what the detected object is in order for it to place it into its correct location.
5.A video demo of the project.

  # Project Plan
# requirement Analysis
  # requirement listing 
  # requirement Specification
  # requirement Standards
# Project Design
  # Conceptual Design
  
  There are three main modules in the project:
a)	Power Module
The power module provides power to four components of the project. The first is the Raspberry Pi and it is provided with a 5 Volts, the second is the Robotic Arm and it is provided by a 5 Volts as well, and the top and pad lights are both provided with 12 Volts. 

b)	Control Module
The control module contains a Raspberry Pi which is acting as the main brain for the project as it is running everything from deep learning model, capturing and processing images, determining arm positioning to controlling buttons and LCD screen. Also, the module contains an Arduino that receives instructions from the raspberry pi to control the robotic arm servos and end-effector. 

c)	I/O Module
The I/O module contains a camera for capturing pictures, an LCD Screen for displaying various critical instructions for the machine, buttons for control, top and pad lights for eliminating noise and color clarity in the pictures, and a robotic arm for sorting the objects. 
	
	The Block diagram below shows the connection between the modules and their components. 

  # Software Design
  # User Interface Design
  # Database Design
  # Algorithm Design
  # Hardware Design
# Implementation
# Testing and Verification
# Conclusions and Future Work
  # Difficulties & Challenges
