cmake_minimum_required(VERSION 3.0.2)
project(scara_robot)

find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  roscpp
  rospy
  sensor_msgs
  std_msgs
  message_generation
)

add_service_files(
   FILES
   inv.srv
   jacob.srv
   inv_jacob.srv
)

generate_messages(
   DEPENDENCIES
   std_msgs
   geometry_msgs
   sensor_msgs
)

catkin_package(
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)

catkin_install_python(PROGRAMS
   scripts/server.py
   scripts/tuner.py
   scripts/vel_servers.py
   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

add_executable(scara_forward src/forward.cpp)
target_link_libraries(scara_forward ${catkin_LIBRARIES})