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


# Project Design 
### 1.Conceptual Design
  
  There are three main modules in the project:
a)	Power Module
The power module provides power to four components of the project. The first is the Raspberry Pi and it is provided with a 5 Volts, the second is the Robotic Arm and it is provided by a 5 Volts as well, and the top and pad lights are both provided with 12 Volts. 

b)	Control Module
The control module contains a Raspberry Pi which is acting as the main brain for the project as it is running everything from deep learning model, capturing and processing images, determining arm positioning to controlling buttons and LCD screen. Also, the module contains an Arduino that receives instructions from the raspberry pi to control the robotic arm servos and end-effector. 

c)	I/O Module
The I/O module contains a camera for capturing pictures, an LCD Screen for displaying various critical instructions for the machine, buttons for control, top and pad lights for eliminating noise and color clarity in the pictures, and a robotic arm for sorting the objects. 
	
	The Block diagram below shows the connection between the modules and their components. 
	![image](https://user-images.githubusercontent.com/63504289/104811552-6b1fd700-580d-11eb-8c36-b5667100e852.png)

 ### 2. Hardware Design
  As a beginning I had few designs, one of them was to have the objects moving on a belt where at a certain position there is a video camera to identify objects and then it goes to a sorting mechanism. For the sorting mechanism I had two designs, the first one is that the belt will have different areas where in front of each one there is a box in which the object belonging to that area is pushed into the box, the second design was at the end of the belt there is a rotating tube that would rotate to the box which the object should go into and then the object would get dropped into that tube to reach the box (Figure 2).These designs were good enough to do the job but they were not approved by my teammate at that time and that is why I didn’t work on them. Finally, I reached to my final design where the object is placed in a certain area which is then picked by a robotic arm to be placed into an object recognition area before being moved into its final destination which is the exact box which it belongs to (Figure 3). 
  
  ![image](https://user-images.githubusercontent.com/63504289/104811586-b1753600-580d-11eb-87bc-cefa6ee6784b.png)
![image](https://user-images.githubusercontent.com/63504289/104811597-c5b93300-580d-11eb-8644-d3e413dee649.png)

•	Raspberry pi:



The raspberry pi was specifically chosen for two reasons. The first one that it has the needed computing power to run a deep learning model that is going to classify the objects. The second reason to is to take pictures by the camera and preprocess them before feeding them to the ML model for the classification.




•	Arduino: 


Arduino is specifically used to control the arm movement and the state of the end-effector as It will perform slightly better in those tasks in comparison with raspberry pie. 



•	Camera:

The camera is needed for capturing images of the objects for detection. 

•	Robotic arm:

Robotic arm was chosen as the main sorting device to take objects from the base position into the recognition areas and finally to the correct position in which each object should go into. 

•	Magnetic solenoid (end-effector):

A magnetic solenoid was specifically chosen for project as the objects that I have designed are made from metal and the magnetic solenoid provide the best mechanism and easiest way of grabbing them. 


•	Top and Pad lights:


After my initial testing of capturing images of the objects I encounter two main issue within the initial design. The first one was that there is too much noise surrounding the objects and thus it makes it very hard to use edge detection for recognizing objects that is why the pad light was necessary to remove all the noise within the area surrounding an object. The second issue was with different light conditions the color of the abject may be different each time and so I wanted to provide enough top light directed to the objects in which the environment lighting conditions doesn’t affect the recognition of the objects.  

  ### 2. Software Design
  ### 3. Algorithm Design
 
# Implementation
# Testing and Verification
# Conclusions and Future Work
