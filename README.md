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
