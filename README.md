# Path Planning Research in Gazebo
---

### **0. Install the Gazebo software**

Gazebo is a robot simulator. Gazebo simulates multiple robots in a 3D environments, with extensive dynamic interaction between objects.

Gazebo Download Link : [http://gazebosim.org](http://gazebosim.org/)

Download and install gazebo. You can go to the website : http://gazebosim.org/install

### **1. Installation**

1. **Development Environment ubuntu 20.04 + [ROS Noetic desktop full](http://wiki.ros.org/noetic/Installation/Ubuntu)**

2. **Build ROS packages for Scout simulator**
    
    Create worksapce, download ROS packages
    ```
    mkdir -p ~/scout_ws/src
    cd ~/scout_ws/src
    git clone https://github.com/kangbeenlee/gazebo-navigation.git
    ```

3.  **Install required ROS packages**
    
    Noetic (ROS version)
    ```
    cd gazebo-navigation
    sh install_dependencies_noetic.sh
    ```

4. **Install dependencies and build**
    ```
    cd ~/scout_ws
    rosdep install --from-paths src --ignore-src -r -y
    catkin_make
    ```

### **2. Simple Test**

1. **SCOUT-MINI description**

    ```
    cd ~/scout_ws
    source devel/setup.bash
    roslaunch scout_description display_scout_mini.launch 
    ```

2. **Launch gazebo simulator and teleop control**
    
    a. Launch gazebo simulator
    ```
    cd ~/scout_ws
    source devel/setup.bash
    roslaunch scout_gazebo_sim scout_mini_playpen.launch
    ```

    b. Run teleop controller (w, a, s, d)
        
    ```
    # Open another terminal
    cd ~/scout_ws
    roslaunch scout_teleop scout_teleop_key.launch 
    ```

### **3. 2D Navigation**

1. **Gmapping SLAM mapping**
    
    ```
    # Run gmapping slam
    roslaunch scout_slam scout_slam.launch
    ```
    ```
    # Save map (in another terminal)
    roslaunch scout_slam gmapping_save.launch
    ```

2. **Navigation**

    EKF is applied to sensor fuse encoder and imu for odometry
    
    ```
    # Run navigation
    roslaunch scout_navigation scout_navigation.launch
    ```