# Spring-2026-Final-Project-Team11
This repository contains all information regarding the DonkeyCar Taxi for team 11.

<h1 align="center">DonkeyCar Taxi using ROS2 and OAK-D Lite</h1>

<br />
<div align="center">
    <img src="images\UCSDLogo_JSOE_BlueGold_Web.jpg" alt="Logo" width="400" height="100">
    <h3>ECE-MAE 148 Final Project</h3>
    <p>
    Team 11 Spring 2026
    </p>
</div>

<div align="center">
    <img src="images\20260610_163807.jpg" width="500" height="400">
</div>
<br>
<hr>


## Table of Contents
  <ol>
<li><a href="#team-members">Team Members</a></li>
    <li><a href="#abstract">Abstract</a></li>
    <li><a href="#Promises">Promises</a></li>
    <li><a href="#accomplishments">Accomplishments</a></li>
    <li><a href="#challenges">Challenges</a></li>
    <li><a href="#final-project-media">Final Project Media</a></li>
    <li><a href="#software">Software</a></li>
        <ul>
        <li><a href="#obstacle-avoidance">Obstacle Avoidance</a></li>
        <li><a href="#object-sign-detection">Object Sign Detection</a></li>
      </ul>
    <li><a href="#hardware">Hardware</a></li>
    <li><a href="#gantt-chart">Gantt Chart</a></li>
    <li><a href="#course-deliverables">Course Deliverables</a></li>
    <li><a href="#project-reproduction">Project Reproduction</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
    <li><a href="#contacts">Contacts</a></li>
  </ol>

<hr>

## Team Members
Alan Ye - ECE [LinkedIn](https://www.linkedin.com/in/alan-ye-683ab6346/)

Wen Qiang - CS

Ryan Melson - MAE [LinkedIn](https://www.linkedin.com/in/ryan-melson-97ab44213/?skipRedirect=true)

<hr>

## Abstract
Our goal for the Final Project was to make a DonkeyCar Taxi, that would bring a passenger, in our case a 3D printed duck, to a valid position to then stop for a short time and simulate a deboarding and boarding process. Using an enhance 2D LiDAR system coincided with an OAK-D Lite for visual confirmation and navigation. Valid parking being designated by a specific sign indicating temporary parking only. 
<hr>

## Promises
* Specific Object detection for allowed parking regions.
* Object / Pedestrian detection using the LiDAR module.
* Get the LiDAR unit operational into ROS2.
<hr>

## Accomplishments
* Navigated a complex network within a Linux environment and ROS2 packages. 
* Implemented a YOLO model to identify and track custom 3D-printed parking signs. 
* Successfully integrated and configured a LiDAR sensor.

## Future Work
If we were to redo this project in the future, it would have been necessary to spend more time learning and creating appropriate documentation on how to operate our LiDAR (see below for type). We would also need to learn how to implement it with an emergency stop feature and visually confirm passengers were on board. Visual confirmation being done with another OAK-D Lite camera with appropriate YOLO model. Being able to identify that it is at a stop and allowing the passenger to safely vacate the vehicle and the car understanding this as well. 
<hr>

## Challenges
* We ran into several component errors and issues leading us to have to delay our progress. As well as outside affairs we couldn't control. 
* LiDAR took a lot longer to learn and understand how it could be implemented into ROS2 than initially expected.
* Time was our biggest struggle especially when only having 3 team members, we all had to take on additional roles to get to the stage we eventually got to. 
<hr>

## Final Project Demo Videos --
Media below shows what we were able to complete for our Final project. 

**Sign Detection Demo** --
[![Sign Detection Demo](https://img.youtube.com/vi/6DFxrUN5yMU/0.jpg)](https://www.youtube.com/watch?v=6DFxrUN5yMU)

**Web UI simulation** --
<a href="[https://youtube.com](https://www.youtube.com/shorts/nQIj7ubcuTM)" target="_blank">
   <img src="[https://youtube.com](https://www.youtube.com/shorts/nQIj7ubcuTM)" alt="Web UI simulation" width="300" />
</a>


**Outside view of robocar driving around compound** --
[![Outside view of robocar driving around compound](https://img.youtube.com/vi/ZWnJwExIKY0/0.jpg)](https://www.youtube.com/watch?v=ZWnJwExIKY0)


**Final Demo** --

[<img src="images\finalDemo.PNG" width="600">](https://drive.google.com/file/d/1g-VeBIl5gdUQflPbHFEFg3UOX2X36orz/view?usp=drive_link)


**Final Clips** -- 

Everything Together (3rd Person)

[<img src="images\everything.PNG" width="300">](https://drive.google.com/file/d/1p2i5tRBihoJaQEioC826KT2X-poMZBU0/view?usp=drive_link)

Everything Together (POV) --

[<img src="images\pov.PNG" width="300">](https://drive.google.com/file/d/1Jt7cPzaUdMSlrA__SZ71dYU6QvQGNySb/view?usp=drive_link)

Obstacle Avoidance --

[<img src="images\earlyAvoid.PNG" width="300">](https://drive.google.com/file/d/1Pd8OklPu9tDEfgzJNNkNkR_zGN-SYbMb/view?usp=drive_link)

Pedestrian Detection --

[<img src="images\personDetected.PNG" width="300">](https://drive.google.com/file/d/11qNUHqOkSNa8mivNA_k-UFk8U7LfdoAp/view?usp=drive_link)

**Early Progress Clips** --

Early Obstacle Avoidance --

[<img src="images\earlierAvoid.PNG" width="300">](https://drive.google.com/file/d/14KP8B8-IEhhGi5ObEtc7LC3ndSPOTO66/view?usp=drive_link)

Early Pedestrian Detection --

[<img src="images\earlyPed.PNG" width="300">](https://drive.google.com/file/d/1O3riZQaE1dmO9sFID_FuAqzC17s5VZ9x/view?usp=drive_link)

<hr>

## Software --

### Overall Architecture --
Our project was completed entirely with ROS2 navigation in python. The 'rclpy' package is being used to control the robot and our primary control logic consists of the Calibration, Person Detection, Lane Detection, Lane Guidance, and nodes.

- The **Calibration Node** was adapted from Spring 2022 Team 1 and updated for our use case. We strictly needed the gold mask to follow the yellow lines and implemented our own lane following code.
  
- The **Person Detection Topic** was fully created for our team's project implementation. The topic is created in our oakd_node.py inside the ucsd_robocar_sensor2_pkg. The oakd_node publishes two topics the first being a color image feed from the camera and the second being an integer value of 1s or 0s for whether it sees a person or not, respectively, using the depth AI's neural network. In order to get the oakd_node running with the rest of the car during navigation a switch must be created in the car_config.yaml file to launch the oakd_launch.launch.py file created in the ucsd_robocar_sensor2_pkg and the previous oakd node must be switched off. The person detection topic is subscribed to in the Lane Guidance Node which ultimately controls the vehicle, while the camera feed is subscribed to in the lane detection node which finds the yellow lines to follow. 

- The **Lane Detection Node** is used to control the robot within the track. We adapt the PID function to calculate the error and set new values to determine the optimal motion of the car to continue following the yellow lines in the lane. This is done by taking the raw camera image, using callibrated color values to detect yellow, and ultimately using the processed image to publish the control values that are subscribed by the lane guidance node.

- Ultimately, the "magic" happens within the **Lane Guidance Node** which is responsible for directly controlling car's movement. We have adapted the Lidar subscription from Spring 2022 Team 1 to detect obstacles within a particular viewing range in front of our car. The lane guidance node subscribes to lane detection node and our Person Detection nodes to correctly traverse the path. If no obstacles are detected, the car will simply continue its line following program, sticking to the yellow lines in the middle of the lane. If an obstacle is detected by the lidar, the car will correspondingly make a turn based on the object's angle and distance. As it routes around the object, the car continues to check for obstacles to avoid any collision and come back to the path. Additionally, if the subscription to the person_detected node is triggered as active, then the car knows there is a pedestrian in view and will stop.

### Obstacle Avoidance --
We used the LD06 Lidar to implement obstacle avoidance within ROS2. The program logic is quite simple in that we are constantly scanning the 60 degrees in front of the robot. If an object is detected within our distance threshold, the robot will accordingly make a turn to avoid it. Our logic for selecting which direction to turn in is quite simple in that if the object is on the left side, we first turn right, and otherwise, we turn left. Both turning directions include a corrective turn to bring the robot back to the centerline of the track and continue lane following.

### Pedestrian Detection --
We used the DepthAI package to implement pedestrian detection within ROS2. We took advantage of the Tiny YOLO neural network setup found within the examples. We filter through the detections to check strictly for a "person" with adjustable confidence levels. We found that a 60% confidence level worked pretty well for our project's use cases. Surprisingly, we found better results with real humans walking in front of the robot (it would detect their feet and be able to classify them as "person" objects). We were also able to successfully scan various printout images of people with high accuracy and success. The programming logic for pedestrian detection is very simple in that if a "person" has been detected in the image passed through by the camera, the VESC throttles are set to 0, stopping the car, until the person has moved out of the field of view.
<hr>

## Hardware 

* __3D Printing:__ All board mounts, Raspberry Pi Mount, Camera Mount and containment.
* __Laser Cutting:__ Base plate to mount electronics and other components.

__Parts List__

* Traxxas Chassis with steering servo and sensored brushless DC motor
* Servo PDB
* Raspberry Pi
* WiFi adapter
* 64 GB Micro SD Card
* Adapter/reader for Micro SD Card
* Logitech F710 controller
* OAK-D Lite Camera
* SICK TiM 2D LiDAR
* VESC
* Anti-spark switch with power switch
* DC-DC Converter
* 4-cell LiPo battery
* Battery voltage checker/alarm
* DC Barrel Connector
* XT60, XT30, MR60 connectors
* USB-C to USB-A cable as well as USB-C to USB-C
* Micro USB to USB cable

__Baseplate__

<img src="images\chassis.png" height="300">

__Rasperry Pi Case/Shell__

<img src="images\rasp_pi.png" height="300">

__Camera Mount__

<img src="images\cam_mount.png" height="300">
<img src="images\camera.png" height="300">

__Circuit Diagram__

<img src="images\circuit.png" height="300">

__Board Mounts__

<img src="images\dcdc_conv.png" height="300">
<img src="images\gps_module.png" height="300">
<img src="images\servo_pdb.png" height="300">

__Parking Sign__

<img src="images\sign.png" height="300">

## Gantt Chart 

<img src="images\gantt.png" height="300">
<hr>

**References:** 
* [Spring 2023 Team 5](https://github.com/UCSD-ECEMAE-148/spring-2023-final-project-team-5) - GitHub Formatting
* [DepthAI](https://github.com/luxonis/depthai-python)
* [UCSD Robocar Framework](https://gitlab.com/ucsd_robocar2)

<hr>

## Contacts 

* Alan Ye (a8ye@ucsd.edu)- ECE [LinkedIn](https://www.linkedin.com/in/alan-ye-683ab6346/)

* Wen Qiang - CS

* Ryan Melson (rmelson@uscd.edu)- MAE [LinkedIn](https://www.linkedin.com/in/ryan-melson-97ab44213/?skipRedirect=true)

