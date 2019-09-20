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
