cmake_minimum_required(VERSION 3.8)
project(kitti_msgs)

# find dependencies
find_package(ament_cmake REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

# for generate messages
rosidl_generate_interfaces(
  ${PROJECT_NAME}
    msg/GeoPlanePoint.msg
  DEPENDENCIES
    std_msgs
    geometry_msgs
)

ament_package()
