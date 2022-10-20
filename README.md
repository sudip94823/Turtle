### 1. Working with Turtlesim

**1.1. Turtlesim Installation**

- To make sure the system is up-to-date
```
sudo apt update 
```
- To install the turtlesim library
```
sudo apt install ros-rolling-turtlesim
```

**1.2. Starting Turtlesim**
```
ros2 run turtlesim turtlesim_node
```

***This command opens up a simulator windows with a random turtle in the center.***

![#2](https://user-images.githubusercontent.com/113494159/192174251-2b255c6e-c634-4acd-9558-6f4a582fd2f1.png)


**1.3. Using Turtlesim**
- The following command is entered in one terminal to control the turtle. 
```
ros2 run turtlesim turtle_teleop_key
```
- Once executed, there should be 3 windows: a terminal running `turtlesim_node`, a terminal running `turtle_teleop_key` and the turtlesim windows.
- We can use the arrow keys on the keyboard to control the direction/movement of the turtle and the path of movement is visible using its attached pen. 

![Turtle](https://user-images.githubusercontent.com/113494159/192175725-eb5d828f-26ec-4c09-a78f-e56ed36dec44.png)

### 2. ROS2 & RQT

**2.1. Installing rqt**

_In the new terminal, codes for installing `rqt` and its plugins are executed:_

```
sudo apt install

sudo apt install ~nros-rolling-rqt*
```
_In order to run rqt, we simply execute `rqt` in the terminal._

```
rqt
```

**2.1.1. Starting rqt Console**

_rqt_console is a GUI tool used to introspect log messages in ROS2._
```
ros2 run rqt_console rqt_console
```

![#4](https://user-images.githubusercontent.com/113494159/192157362-ff19aa73-21f4-4dd0-8269-9eadd3180303.png)



**2.2. Use rqt**

_Once rqt command is initialized, a blank window is popped up. We have to select **Plugins > Services > Service Caller** from the menu bar at the top._

![#3](https://user-images.githubusercontent.com/113494159/192157358-b07e4bb3-2891-4b0f-8369-ff4241ee19ac.png)

_By clicking on the **Service** dropdown list, we can see the various turtlesim's services, among which we willl be doing two services here as follows:_

**2.2.1. Trying the spawn service**

First of all, we can use rqt to call the `/spawn` service which will create another turtle in the turtlesim window.

We can provide unique name to the turtle, for example here `Sudip` from the **Expression** column and also we have to provided certain coordinates for the turtle to spawn , like `x=5.9` and `y=3.0` as shown in the image below. 

![#5](https://user-images.githubusercontent.com/113494159/192176295-2c9a0cf5-2442-4835-a402-482695e1b519.png)


**2.2.2. Trying the set-pen service**

This service is used to give the turtle it's unique color and width of pen while it moves by using `/set_pen` service.

The value for `r`, `g`, `b` can be set anywhere between 0 and 255 which will set the color of the pen and the `width` gives the thickness of the line.

![image](https://user-images.githubusercontent.com/113494159/195586596-e84297f4-0d50-4e46-b481-a1d4e89ccf0e.png)

_Here in this first image, **r** is set to 255 and others are 0 so the line is **red** and in the second image its the same case but **b** is set to 255 and others are 0 so the line is **blue** instead of red. _ 

![image](https://user-images.githubusercontent.com/113494159/195586769-9f521316-cdb0-4e8d-87cc-542f3a927ea7.png)



**2.3. Remapping**

Remapping is used when we have to move the second turtle as well. We can do that by remapping turtle1's `cmd_vel` topic onto second turtle. 

In the new terminal, we have to source ROS2 and run the following command:

```
ros2 run turtlesim turtle_teleop_key --ros-args --remap turtle1/cmd_vel:=turtle2/cmd_vel
```

Now we can move second turtle when this terminal is active and turtle1 when the other terminal running the `turtle_teleop_key` is active.


**2.4. Close turtlesim**

In order to stop the simulation, `Ctrl + C` will do the task or press `q` in the teleop terminal.


### 3. Understanding the Basic concepts
- ROS2 Nodes
- ROS2 Topics
- ROS2 Services
- ROS2 Parameters
- ROS2 Actions


### 4. ROS2 Colcon

**4.1. Installing Colcon**
```
sudo apt install python3-colcon-common-extensions
```


**4.2. Breifing on ROS Workspace**


- ROS Workspace is the directory having a particular structure and by default it create the following directories : `src`, `build`, `install` and `log`.
- **build** directory stores intermediate files. 
- **install** directory is where the packages are installed.
- **log** directory stores various logging information


### 5. Creating a Workspace


**5.1. Firstly, we need to create a directory to contain our workspace and the directory is named: `ros2_ws`**


```
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
```

_This will create a workspace which contains a single empty directory `src`. So we need to add some sources_

```
git clone https://github.com/ros2/examples src/examples -b foxy
```
_Now the workspace have source code to the ROS 2 examples._

**5.2. Building the Workspace**


**In the root of the workspace, we run the `colcon build`. After the build is finished, we can see 3 more directories: `build`, `install`, and `log`.**

```
colcon build --symlink-install
```

**5.3. Running Tests**
```
colcon test
```

**5.4. Source the Environment**

It is a important before we can run executables built by colcon. 

```
. install/setup.bash
```
