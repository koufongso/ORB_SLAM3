# ORB-SLAM3

This is the RB5 development branch. It was used to run on RB5 without the GUI systems/components. 

# 2. Prerequisites
This is based on RB5 image QRB5165.UBUN.1.0-210512 (18.04 dev kernal).

## C++11 or C++0x Compiler
I am currently compiling with C++14

## RealSense SDK

It was tested with D455 camera.

Need to install realsense SDK if want to use D435i/D455 GRB-D camera, follow installation insturctions [here](https://dev.intelrealsense.com/docs/compiling-librealsense-for-linux-ubuntu-guide#building-librealsense2-sdk).


## RealSense ROS wrapper

Running on ROS1 (melodic), please follow installation instruction [here](https://github.com/IntelRealSense/realsense-ros/tree/ros1-legacy)

## OpenCV
We use [OpenCV](http://opencv.org) to manipulate images and features. Dowload and install instructions can be found at: http://opencv.org and tested with OpenCV 3.2. 

## Eigen3
Required by g2o (see below). Download and install instructions can be found at: http://eigen.tuxfamily.org. **Required at least 3.1.0**.

## DBoW2 and g2o (Included in Thirdparty folder)
We use modified versions of the [DBoW2](https://github.com/dorian3d/DBoW2) library to perform place recognition and [g2o](https://github.com/RainerKuemmerle/g2o) library to perform non-linear optimizations. Both modified libraries (which are BSD) are included in the *Thirdparty* folder.

## Python
Required to calculate the alignment of the trajectory with the ground truth. **Required Numpy module**.

* (win) http://www.python.org/downloads/windows
* (deb) `sudo apt install libpython2.7-dev`
* (mac) preinstalled with osx

## sophus (ROS)
```
sudo apt-get install ros-melodic-sophus
```

# 3. Building ORB-SLAM3 library and examples

Clone the repository, and run:

```
cd ORB_SLAM3
chmod +x build.sh
./build.sh
```

This will create **libORB_SLAM3.so**  at *lib* folder and the executables in *Examples* folder.

# 4 Building ORB-SLAM3 ROS 
```
cd PATH/ORB_SLAM3
source /opt/ros/melodic/setup.bash
export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:PATH/ORB_SLAM3/Examples/ROS
./build_ros.sh
```

# Run ORB-SLAM3 ROS

```
#Run ORB_SLAM3 (ROS)

source /opt/ros/melodic/setup.bash
export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:PATH/ORB_SLAM3/Examples/ROS
roslaunch ORB_SLAM3 launch_d455.launch
```
```
#Run ORB_SLAM3 (ROS)

source /opt/ros/melodic/setup.bash
export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:/home/gfs/ORB_SLAM3/Examples/ROS
roslaunch ORB_SLAM3 launch_d455.launch
```

```
#Run D455

cd PATH_TO_realsense_ws
source devel/setup.bash
roslaunch realsense2_camera rs_camera.launch enable_infra1:=true enable_infra2:=true enable_accel:=true enable_gyro:=true unite_imu_method:=linear_interpolation enable_depth:=false enable_color:=false
```
