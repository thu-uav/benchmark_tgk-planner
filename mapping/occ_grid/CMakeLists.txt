cmake_minimum_required(VERSION 2.8.10)
project(occ_grid)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -Wall")
set(CMAKE_CXX_STANDARD 14)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  visualization_msgs
  message_filters
  poly_traj_utils
  cv_bridge
  tf2_ros
  tf2
)

find_package(OpenCV REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(PCL 1.7 REQUIRED)

catkin_package(
 INCLUDE_DIRS include
 LIBRARIES occ_grid
 CATKIN_DEPENDS roscpp std_msgs 
#  DEPENDS system_lib
)

include_directories( 
    include 
    ${catkin_INCLUDE_DIRS}
    ${PCL_INCLUDE_DIRS}
    ${OpenCV_INCLUDE_DIRS}
    ${Eigen3_INCLUDE_DIRS}
)

link_directories(${PCL_LIBRARY_DIRS})
link_directories(${OpenCV_LIBRARIES})

add_library( occ_grid 
    src/occ_map.cpp 
    src/raycast.cpp
    src/pos_checker.cpp
)

target_link_libraries( occ_grid
    ${catkin_LIBRARIES}
    ${PCL_LIBRARIES}
    ${OpenCV_LIBRARIES}
)  
