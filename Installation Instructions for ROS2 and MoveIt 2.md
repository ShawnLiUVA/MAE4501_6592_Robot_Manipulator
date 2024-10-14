# Installation Instructions for ROS2 and MoveIt 2

These instructions will guide you through installing **ROS 2 Humble Hawksbill** and **MoveIt 2** on **Ubuntu 22.04 LTS (Jammy Jellyfish)**.

---

## Prerequisites

- **Operating System**: Ubuntu 22.04 LTS
- **User Privileges**: You need sudo (administrator) privileges.

## Step 1: Set Up Sources and Keys

### 1.1 Add the ROS 2 GPG Key

Open a terminal and run:

`sudo apt update sudo apt install -y curl gnupg lsb-release sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -`

### 1.2 Add the ROS 2 Repository

`sudo sh -c 'echo "deb [arch=$(dpkg --print-architecture)] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list'`

## Step 2: Install ROS 2 Humble Hawksbill

### 2.1 Update Package Index

`sudo apt update`

### 2.2 Install ROS 2 Packages

Install the full desktop version, which includes RViz, demos, and tutorials:

`sudo apt install -y ros-humble-desktop`

*Alternatively*, you can install a smaller set:

- **Desktop**: `sudo apt install -y ros-humble-desktop`
- **ROS-Base (Bare Bones)**: `sudo apt install -y ros-humble-ros-base`

## Step 3: Environment Setup

### 3.1 Source the Setup Script

To automatically source ROS 2 environment variables in every terminal:

`echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc source ~/.bashrc`

*Alternatively*, source the script in each new terminal:

`source /opt/ros/humble/setup.bash`

## Step 4: Install Development Tools and Dependencies

### 4.1 Install Essential Tools

`sudo apt install -y python3-pip python3-colcon-common-extensions python3-rosdep`

### 4.2 Initialize `rosdep`

`sudo rosdep init rosdep update`

## Step 5: Install MoveIt 2

### 5.1 Install MoveIt 2 Packages

`sudo apt install -y ros-humble-moveit`

### 5.2 Install Additional Dependencies

`sudo apt install -y ros-humble-ros2-control ros-humble-ros2-controllers`

## Step 6: Verify Installations

### 6.1 Test ROS 2 Installation

Open a terminal and run the talker node:

`ros2 run demo_nodes_cpp talker`

In another terminal, run the listener node:

`ros2 run demo_nodes_cpp listener`

You should see messages being published and received between the nodes.

### 6.2 Test MoveIt 2 Installation

#### 6.2.1 Launch the MoveIt 2 Demo

`ros2 launch moveit2_tutorials demo.launch.py`

#### 6.2.2 Visualize in RViz2

- RViz2 should open displaying a robot model.
- Use the MotionPlanning panel to interact with MoveIt 2.

## Step 7: Additional Configuration (Optional)

### 7.1 Install ROS 2 Package for UR5

If you're working with the UR5 robot, install the Universal Robots ROS 2 driver:

`sudo apt install -y ros-humble-ur-robot-driver`

### 7.2 Clone Example Packages

Set up a workspace:

`mkdir -p ~/ros2_ws/src cd ~/ros2_ws/src`

Clone necessary repositories:

`git clone -b humble https://github.com/UniversalRobots/Universal_Robots_ROS2_Driver.git git clone -b humble https://github.com/ros-industrial/universal_robot.git`

Install dependencies:

`cd ~/ros2_ws rosdep install --from-paths src --ignore-src -r -y`

Build the workspace:

`colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release`

Source the workspace:

`echo "source ~/ros2_ws/install/setup.bash" >> ~/.bashrc source ~/.bashrc`

## Step 8: Launch MoveIt 2 with UR5 (Optional)

`ros2 launch ur_moveit_config ur_moveit.launch.py ur_type:=ur5 robot_ip:=<robot_ip> use_fake_hardware:=true launch_rviz:=true`

- Replace `<robot_ip>` with your robot's IP address.
- If you don't have a physical robot, set `use_fake_hardware:=true`.

## Step 9: Additional Resources

- **ROS 2 Documentation**: https://docs.ros.org/en/humble
- **MoveIt 2 Tutorials**: https://moveit.picknik.ai/humble/doc/tutorials/getting_started/getting_started.html
- **Universal Robots ROS 2 Driver**: [GitHub - UniversalRobots/Universal_Robots_ROS2_Driver: Universal Robots ROS2 driver supporting CB3 and e-Series](https://github.com/UniversalRobots/Universal_Robots_ROS2_Driver)

---

Now you have ROS 2 Humble Hawksbill and MoveIt 2 installed on your Ubuntu 22.04 LTS system. You can proceed to develop and simulate advanced robotic applications using the UR5 robot arm.


