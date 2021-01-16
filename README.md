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
  I designed the software to have one main script and 3 classes as follows: 
#### 1.	A Main script that works as follows: 

	1.	When the script starts the first thing it checks is whether the Deep learning model is loaded or not, if it doesn’t load then it will stop otherwise it will continue.
	![image](https://user-images.githubusercontent.com/63504289/104811774-f057bb80-580e-11eb-80c8-9a17969a6ae0.png)

	2.	It will then check if the serial connection has been established with the Arduino, again here if the connection is not established then it will stop otherwise will continue. 
	![image](https://user-images.githubusercontent.com/63504289/104811777-f5b50600-580e-11eb-9eea-a1e0320216f5.png)

	3.	Now that everything is loaded and connected it will initialize the robotic arm in the ready position and start initialize the conditional variable needed for the different states of the machine. 
	![image](https://user-images.githubusercontent.com/63504289/104811781-fd74aa80-580e-11eb-961e-8e65c454ce31.png)

	4.	Now the scrip will enter a while(true) loop (infinite loop) that will only be exited if shutdown sequence is detected. 

	5.	Inside the loop we are waiting for a button to be pressed either the start or the pause buttons.


		A.	If start button is pressed then we have to conditions: either it is the first time the machine is run and we want to print ( starting) on the LCD display, or the machine is already started and have been paused and we want to print (Resuming) on the LCD display 
		B.	If pause button is pressed, we want to set the conditional variable of the machine to tell it that it is paused and shouldn’t do anything until it is started again. 

	6.	Next, we check if the machine is already started and haven’t been paused ? 

		A.	if no then it means the machine is paused and we have two conditions: either it’s the first time to be paused after being at work and we want to print paused on the display and set the machine in the waiting position Or the machine have been paused and waiting already and the pause button was pressed again which activates a shutdown and thus we want to break out of the loop. 
		B.	If yes then we want to take care of the arm position between base position, detection positions and object sorting location. 

	7.	After a position have been determined we tell the Arduino exactly how we want the arm to move 

	8.	After moving the arm to the desired location, we check the detection condition:

		A.	if it is true then we want to take a picture then preprocess it and prepare it then feed it into our model:

			o	if the model predicts an object correctly then we want to set the detection condition to false and print the object name on the LCD display. 
			o	if there was an exception then it means that there is no object on the pad and we want to pause the machine. 

		B.	If it is False then we do nothing. 

	9.	Next, we check if grab object condition is true: 

		A.	If True then we need to tell the Arduino to send a high voltage to the end-effector. 
		B.	If False then we will tell the Arduino to send a low voltage to the end-effector. 

	10.	The loop then starts again.

The Flow Chart below demonstrates the main script 
![image](https://user-images.githubusercontent.com/63504289/104811684-4710c580-580e-11eb-8a17-1c00f503b1ce.png)

#### 2.	A Class for capturing images: (Look at capture.py)

#### 3.	A class for preprocessing and preparing the images before feeding them to the model: (Look at processing.py)

#### 4.	A class that holds the name and position of the predicted objects: (Look at positions.py)

  ### 3. Algorithm Design
  There are 3 main states that the arm takes while moving the objects as follows:
1.	There is nothing on the pad being detected and we want to pick the object from the base to the pad . 
2.	There is an object on the pad that we need to detect and a new object on the pad that needs to be picked for detection. 
3.	There are two objects on the pad one of which finished detection and needs to be sorted. 

To handle the position of the arm between the three states we check the states of the currentPosition and nextPosition variables which are initialized to “pick first” and “drop first”. One thing to note is that there two positions for detection and “first” & “second” in the currentPosition or nextPosition means an object to be dropped in first or second detection locations unless stated otherwise. There are six conditional arguments to handle the arm between the three states and they work as follows: 

1.	If the currentPosition is “pick first” then we check if the nextPosition is “drop first” or “drop detected” ? 

o	If True then it means that either we don’t have any object on the pad or there is an object that has been detected and needs to be sorted. In both cases we want to move to the base to grab an object and drop it in the pad for detection by changing the currentPosition to “drop first”

o	If False then it means that both detection locations are occupied and we need to sort the object that has been detected already before we pick a new object. And we do this by changing the currentPosition to “drop detected” 

2.	If the currentPosition is “drop first” then it means we already picked an object that we want to drop in the first detection location and we do so. Then we check if the nextPosition is “drop first” ? 

o	If yes then it means that we finished dropping it then and we want to set the currentPosition to “detect” as we want to detect the object that we have just dropped as well as setting the nextPosition to “pick second” so that we pick another object for detection. 

o	If No then it means we already finished detecting the object and we want to set the currentPosition to “pick second”

3.	If the currentPosition is “detect” then it means the pad now only has one object and we want to detect it and we want to pick a second object for detection. First, we will move the arm to the base for picking a second object and the detect variable will be set to “true”. Next, we check the nextPosition :

o	If it is “pick second” then it means we are going to detect an object in the first detecting location and we want to pick a second object. So, we set currentPosition to “pick second”

o	If it is not then it means that either we just sorted an object that was in the first detection location or in the second and we need to check the nextPosition to determine that: 
-	If the nextPosition is “detect first” then it means that we just sorted an object that was in the second location and we want to pick another object to be dropped in the same location. So, we will set the currentPosition to “ pick second” and nextPosition to “drop second” .

-	If it is not then it means that we just sorted and object that was in the first location. So, we set currentPosition to “pick first” and the nextPosition to “drop detected”.

4.	If the currentPosition is “pick second” then we want to check weather nextPosition is “detect first” ?

o	If yes then means that we have actually already dropped an object in the second location and second here means “a second object”  that should be dropped in the first detection location so we want to move to the base position to pick an object then we will set the currentPosition to “detect” so that we detect the object in the first detection location and nextPosition to “pick first”. 

o	If No then we want to cheack if the nextposition is “drop detected” ? 

-	If yes then it means that both detecting locations are full and we want to take the object in the second detection location to its sorting location and set currentPosition to “drop detected” and nextPosition to “detect first”  

-	If No then it means that an object in the first detection location has been detected and we want to drop a new object in the second detection location then handle sort the detected object. So, we pick the new object then we set the currentPosition to “drop second” and the nextPosition to “detect second”

5.	If the currentPosition is “drop second” then we want to move to second detection location and drop the object in hand then set current position to “pick first” 

6.	If the currentPosition is “drop detected” then it means that we already picked an object that has been detected and so we need to move to its sorting location and drop it then we will set currentPosition to “detect” so that we detect the object that is in the pad currently. 

Figure 5 below contains a chart of the previous steps 
![image](https://user-images.githubusercontent.com/63504289/104811736-aa9af300-580e-11eb-8a2c-3501a0f729ef.png)

 
# Implementation
# Testing and Verification
# Conclusions and Future Work
