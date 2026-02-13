# Autonomous-Waiter-Robot-Simulations

## How to run:

### 1. System Requirements:
* **Host System:** Windows 11 
* **Development Environment:** Ubuntu 22.04.4 LTS running via WSL (Windows Subsystem for Linux) 
* **ROS2 Distribution:** Humble 
* **Simulation Tools:** 
  * Gazebo for simulation
  * RViz for visualization

### 2. Step-by-Step Instructions:
* **Locate and click on the dev_ws.zip file.**
* **Click the Download button to download the zipped folder to your local machine.**
![image](https://github.com/user-attachments/assets/5982f975-0af5-4438-8aba-76d0b671be13)

### 3. Extract the Folder
* **After downloading, extract the dev_ws.zip folder to a desired location on your system**
* **Set UP the Development Workspace in WSL**
  * Open WSL (Ubuntu 22.04.4 LTS in my case).
  * Navigate to the dev_ws directory.
  * To ensure that the contents of the dev_ws folder are as expected, use this command lists the contents of the current directory. It should display files like src/, install/, build/, etc.
   ```bash
   ls
   
 ![image](https://github.com/user-attachments/assets/29551d91-970f-4f1d-b05a-bb4943b285df)

### 4. Running the Simulation
To start the simulation run the following command in your terminal:
```bash
ros2 launch my_bot launch_sim.launch.py
 ```
* This command will launch the simulation in Gazebo, opening a virtual space environment where the Autonomous Waiter Robot will be placed.
* Once the command is executed, you should see Gazebo running with the robot in a 3D simulated environment.
![image](https://github.com/user-attachments/assets/cf3954c4-c731-4026-a60f-7ab2323c5b9f)

### 5. Controlling the Robot
By default, the robot will placed in the environment, but it will not move. To control the robot’s movements, you need to open a second Terminal and run the following command:
```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```
* This command will allow you to control the robot using the keyboard.
* You can navigate the robot and control its speed using the arrow keys on your keyboard.
* **Note:** The terminal running the teleop_twist_keyboard command must remain active and open in order for the controls to work. If the terminal is closed or minimized, the robot will not respond to movement commands.
* Once the terminal is running, you can use the following keys to control the robot:
  * I: Move the robot forward.
  * L: Turn the robot right.
  * J: Turn the robot left.
  * K: Stop the robot.
    
**Here is a link for running teleop_twist_keyboard with Gazebo:** https://youtu.be/FbXKk7vDK7c

### 6. Running RViz2 for Visualization
To visualize the robot and the simulation environment, you need to run RViz2 in a separate terminal. Follow these steps:
   1.	Open a new terminal “don’t close any previous terminal”
   2.	Run the following command:
   ```bash
   rviz2
```  	
* This will launch RViz2, a 3D visualization tool, where you can see the robot and its surroundings the simulation.
* In RViz2, you will be able to visualize the robot’s sensor data, its path, and other relevant information.

![image](https://github.com/user-attachments/assets/1f27155a-6555-44a4-916f-663ae282c2bf)

**In RViz2 in the left side put the Fixed Frame to the base_link**

![image](https://github.com/user-attachments/assets/2220d6f8-bc1e-4363-a42d-d502d05359b5)

**After testing RViz2 and Gazebo press Ctrl+C in all the opened terminals to terminate the processes.**

### 7.	Launching the Simulation with a Custom Map
To run the simulation with our map, use the following command:
```bash
ros2 launch my_bot launch_sim.launch.py world:=our_resaurant
```
*	our_resaurant is the name of our restaurant map, and it is located in the dev_ws folder. 
*	This command will launch the simulation in Gazebo with the specified map, allowing the robot to interact with the environment you have created.

After launching the simulation with your custom map, you can control the movement of the robot as described in Section 5.

![image](https://github.com/user-attachments/assets/3899ed22-0aed-4c86-a000-65dca704cb89)

Here is a video of moving the robot in the restaurant: https://youtu.be/-mGuK7URsVk

### 8.	Running Mapping with SLAM ToolBox
To begin the SLAM process and create a map of the environment, use the following command in a new terminal:
```bash
ros2 launch slam_toolbox online_async_launch.py use_sim_time:=true
```
*	This command will start SLAM Toolbox, which will allow the robot to build a map of the environment in real time.
**Important Notes:**
*	Keep the following terminals running:
1.	Terminal 1: Run the command to launch the simulation with map (as explained in Section 7)
2.	Terminal 2: Run teleop_twist_keyboard to control the robot's movement (as explained in Section 5).
3.	Terminal 3: Run rviz2 to visualize the environment and the robot in RVize2 (as explained in Section 6)
4.	Terminal 4: Run the SLAM Toolbox command: **ros2 launch slam_toolbox online_async_launch.py use_sim_time:=true**
*	This setup will allow you to control the robot’s movement, visualize the map being created, and see the robot’s position in real-time.
**As shown in the figure below:**
1: is for rviz2
2: is for teleop_twist_keyboard
3: is for SLAM Toolbox
4: is for launch the simulation with map

![image](https://github.com/user-attachments/assets/0342906b-49a7-44eb-96d1-0682b63e1f30)

**You will notes that the RVize2 start showing map as shown in the figure below:**

![image](https://github.com/user-attachments/assets/997f1581-0203-4554-bbbc-17606096aba1)

**Here is a video link showing the mapping process:** https://youtu.be/T0uWB3VfGJA

### 9.	Running Navigation with Nav2
To enable the robot to navigate to specific positions or tables, you need to launch Nav2. Use the following command in a new terminal:
```bash
ros2 launch nav2_bringup navigation_launch.py use_sim_time:=true
```
*	This command will start the Nav2 Navigation Stack, which allows the robot to navigate through the environment using the map and sensors.
*	Once Nav2 is running, you can command the robot to move to any poison or table within the restaurant map.
**Important Notes:**
*	Run these terminals:
   1.	Terminal 1: Run the command to launch the simulation with map (as explained in Section 7)
   2.	Terminal 2: Run teleop_twist_keyboard to control the robot's movement (as explained in Section 5).
   3.	Terminal 3: Run rviz2 to visualize the environment and the robot in RVize2 (as explained in Section 6)
   4.	Terminal 4: Run the SLAM Toolbox command: ros2 launch slam_toolbox online_async_launch.py use_sim_time:=true
   5.	Terminal 5: run Nav2 using this command: ros2 launch nav2_bringup navigation_launch.py use_sim_time:=true
*	Ensure to set Fixed Frame to map in RViz2:
  
 ![image](https://github.com/user-attachments/assets/ca8adaed-bc64-4e3f-a7ed-a6766e7177b2)

 * Start by manually exploring the environment using the keyboard teleoperation tool.
*	Navigate the robot around the area until a complete map is generated.
*	Set the Navigation Goal:
    * In RViz2, locate the "2D Goal Pose" tool at the top toolbar.
    *	Select the "2D Goal Pose" tool and click on the map at the position where you want the robot to navigate.
    *	Drag the arrow to indicate the direction the robot should face upon reaching the goal.

![image](https://github.com/user-attachments/assets/3bde1889-48e4-4419-a0fa-4257cf6e8ad5)

***The robot will begin navigating towards the specified position while avoiding obstacles.***

**Here is a video link for the Navigation:** https://youtu.be/OzYP6ZJatYw


## Acknowledgments

The simulation was built with the help of this excellent tutorial series:  
[Building a mobile robot on YouTube](https://www.youtube.com/playlist?list=PLunhqkrRNRhYAffV8JDiFOatQXuU-NnxT).



