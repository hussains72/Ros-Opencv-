# Ros-Opencv-
## Working With ROS and OpenCV in ROS Melodic  

ROS Melodic generally supported OpenCV version 3.x.  
ROS Noetic typically had support for OpenCV version 4.x.   

Jetson nano has opencv 4 installed in it.

create a new package named cv_basics  

mkdir -p ~/catkin_ws/src  

cd ~/catkin_ws/src  

catkin_create_pkg cv_basics image_transport cv_bridge sensor_msgs rospy roscpp std_msgs

### Create the Image Subscriber Node (C++)  

cd ..  

source devel/setup.bash  

 echo $ROS_PACKAGE_PATH
/home/sajid/catkin_ws/src:/opt/ros/melodic/share  

roscd cv_basics/src  


Open a new C++ file named webcam_pub_cpp.cpp.  

gedit webcam_pub_cpp.cpp



roscd cv_basics  


gedit CMakeLists.txt  

find_package( OpenCV REQUIRED )  

include_directories(
  
  /usr/include/opencv4  # Add this line to specify the OpenCV include directory
)  

add_executable(webcam_pub_cpp src/webcam_pub_cpp.cpp)  
target_link_libraries(webcam_pub_cpp ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})

Run the following command in your terminal to create the symbolic link:  
sudo ln -s /usr/include/opencv4 /usr/include/opencv  

This command creates a symbolic link named opencv in the /usr/include directory, which points to the opencv4 directory. This should resolve the issue for cv_bridge by redirecting the expected /usr/include/opencv to the actual OpenCV 4 include directory.  

cd ~/catkin_ws  

catkin_make  

## Run the Image Publisher Node (C++)  

roscd cv_basics/src  

gedit webcam_sub_cpp.cpp  

roscd cv_basics  

gedit CMakeLists.txt  

add_executable(webcam_sub_cpp src/webcam_sub_cpp.cpp)  
target_link_libraries(webcam_sub_cpp ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})  

cd ~/catkin_ws  

catkin_make  

roscd cv_basics/launch  

gedit cv_basics_cpp.launch  


roslaunch cv_basics cv_basics_cpp.launch




