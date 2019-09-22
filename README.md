# eyerobot-project-self-using
Tutorial for using EyeRobot 2.0 &amp; 2.1
# 1. two PC sychronize
for the modified PC
```bash
$ cd ./eye_robot
$ git status
$ git commit -a -m "some useful comments"
$ git push
```
for the unmodified PC
```bash
$ git pull
```
if emerge conflicts occur, delete one of them
* Find the position of "<<<<<<"
* We will have a such a structure
```bash
<<<<<< head
conflict 1
========
conflict 2
<<<<<<<
```
* Just delete one of them (conflict 1 & 2) depending on your case
* Finally, we should activate this repository
```bash
$ catkin build eye_robot_example
```
# 2. differnet tool tip offset should be noted
In order to know the position of tool's tip, it's necessary to tell the PC the distance between the mechanical RCM point and the tip
* open the related file
```bash
$ subl address/ robotControlUI.fl
```
* search "TipOffset"
* change the value which is depend on the tool

# 3. differnet tool name should be noted
* we can see the tool name in GUI --> Tip Force --> Tool "Name"
* search FBGSensor/code/devFBGSensor.h
* in the code, change "#define Tool_NO"
* for dual sensor, number series is 9-4-3-3 (from N-SENSORS --> N-CHANNELS)
* for only tip sensor, number series is 3-2-1-3 (from N-SENSORS --> N-CHANNELS)

# 4. if we make a new FBG tool
* the simplest way is to overwrite the existing useless one
* change the calibration matrix in decFBGSensor.cpp

# 5. "Logger" function
* click Logger
* write the file name
* press SetFileName 
* the file is saved in Home/storage/exp/robot

# 6. Cisst communicate with ROS
* eye-robot-example/eye-robot-example/main.cpp
* go to "ros bridge”
* in mtsCISSTToRos.h find the corresponding Cisst msg and ROS msg

# 7. robotversion
* Home/catkin_ws/src/eye_robot/robotVersion.h

# 8. Start ClipCannula
```bash
$ rostopic pub /eyebot2/ForceRebiasFlag std_msgs/Int32 1
```
* 1 for tip on, 2 for tip off
* click Forcesensor in GUI
* click rebias

# 9. Using the microscope
* first set the microscope in a suitable place
* integrate a camera on the microscope
* strat a software named as "coriander"
```bash
$ sudo coriander
```
* then press "service" --> "display"
*save video
```bash
$ cd storage/
$ cd exp/
$ cd vedieos/
$ ./ssr
```

# 10. Qt creater tip
* ctrl + function name
* ctrl + variable

# 11. mode CM_SLAVE
* connect two pc by a physical Ethernet cable
* open .bashrc
```bash
$ gedit .bashrc
```
* choose the required ROS_MASTER_URI (first for bilateral control, second for single robot)
* open robotTask.cpp
* change the following code
```bash
InitEyeRegister = false;
InitRobotRegister = false;
```
to
```bash
InitEyeRegister = true;
InitRobotRegister = true;
```
* then press the button "SlaveButton"
* start registration
* if you want to change the registeration numbers
* cahnge it in robotControlAlgorithm.h
```bash
NumEyeRegisterData 32;
NumRobotRegisterData 32;
```

# 12. tip for rcm calibration
* for eyerobot 2.1, the measured length should minus 23.45 mm
