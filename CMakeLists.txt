cmake_minimum_required(VERSION 3.5)
project(gazebosensorplugins)

# Options for Qt
# set(CMAKE_AUTOMOC ON)
# set(CMAKE_AUTOUIC ON)

# SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -std=c++11")


# add_definitions(-std=c++11)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
# find_package(catkin REQUIRED COMPONENTS
#   gazebo_ros
#   roscpp
#   std_msgs
#   gtec_msgs
#   tf
# )

# find dependencies
find_package(ament_cmake REQUIRED)

find_package(gazebo_ros_pkgs REQUIRED)
find_package(std_msgs REQUIRED)
find_package(visualization_msgs REQUIRED)
find_package(gtec_msgs REQUIRED)
find_package(tf2 REQUIRED)
find_package(gazebo_ros REQUIRED)

# Depend on system install of Gazebo
find_package(gazebo REQUIRED)

link_directories(${GAZEBO_LIBRARY_DIRS})
include_directories(${Boost_INCLUDE_DIR} ${ament_cmake_INCLUDE_DIRS} ${GAZEBO_INCLUDE_DIRS})

add_library(gtec_uwb_plugin src/UwbPlugin.cpp)
ament_target_dependencies(gtec_uwb_plugin
  gazebo_ros_pkgs
  std_msgs
  visualization_msgs
  gtec_msgs
  tf2
  gazebo_ros
)

install(
  TARGETS gtec_uwb_plugin
  DESTINATION lib/${PROJECT_NAME}
)

ament_package()

# target_link_libraries(gtec_uwb_plugin ${colcon_LIBRARIES} ${GAZEBO_LIBRARIES} ${Boost_LIBRARIES})
# add_dependencies(gtec_uwb_plugin ${colcon_EXPORTED_TARGETS})

# add_library(gtec_magnetic_distortion_plugin src/MagneticDistortionPlugin.cpp)
# target_link_libraries(gtec_magnetic_distortion_plugin ${colcon_LIBRARIES} ${GAZEBO_LIBRARIES} ${Boost_LIBRARIES})
# add_dependencies(gtec_magnetic_distortion_plugin ${colcon_EXPORTED_TARGETS})

# add_library(custom_skid_steer_drive src/CustomSkidSteerDrive.cpp src/CustomSkidSteerDrive.h)
# target_link_libraries(custom_skid_steer_drive ${colcon_LIBRARIES} ${GAZEBO_LIBRARIES} ${Boost_LIBRARIES})
# add_dependencies(custom_skid_steer_drive ${colcon_EXPORTED_TARGETS})

# add_library(gtec_tag_pos_publisher_plugin src/TagPosPublisherPlugin.cpp)
# target_link_libraries(gtec_tag_pos_publisher_plugin ${colcon_LIBRARIES} ${GAZEBO_LIBRARIES} ${Boost_LIBRARIES})
# add_dependencies(gtec_tag_pos_publisher_plugin ${colcon_EXPORTED_TARGETS})

# catkin_package(
#   DEPENDS 
#     roscpp 
#     gazebo_ros
#     gtec_msgs
# )
##add_dependencies(${PROJECT_NAME} gtec_generate_messages_cpp)
