cmake_minimum_required(VERSION 3.20)
project(kitti_msgs)

# Default to C++17
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 17)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
# uncomment the following section in order to fill in
# further dependencies manually.
# find_package(<dependency> REQUIRED)
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

# Get the generated C++ typesupport target
rosidl_get_typesupport_target(cpp_typesupport_target
  "${PROJECT_NAME}" "rosidl_typesupport_cpp")

# Create an interface library that downstream can link against
# via ${kitti_msgs_TARGETS}
if(TARGET "${cpp_typesupport_target}")
  add_library(${PROJECT_NAME}_library INTERFACE)
  target_link_libraries(${PROJECT_NAME}_library INTERFACE
    "${cpp_typesupport_target}")

  install(
    TARGETS ${PROJECT_NAME}_library
    EXPORT export_${PROJECT_NAME}
  )

  # Export modern CMake targets — this is what populates
  # ${kitti_msgs_TARGETS} for downstream packages
  ament_export_targets(export_${PROJECT_NAME})
endif()

ament_export_dependencies(rosidl_default_runtime)

ament_package()
