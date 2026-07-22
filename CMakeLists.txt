cmake_minimum_required(VERSION 3.20)
project(av_msgs)

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

# Generate messages
rosidl_generate_interfaces(
  ${PROJECT_NAME}
    msg/GeoPlanePoint.msg
    msg/LaneExistence.msg
  DEPENDENCIES
    std_msgs
    geometry_msgs
)

ament_package()
