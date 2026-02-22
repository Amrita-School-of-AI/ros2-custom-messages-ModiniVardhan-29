cmake_minimum_required(VERSION 3.8)
project(ros2_custom_msgs)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

# Generate custom message
rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/RobotStatus.msg"
)

# Create executable
add_executable(status_publisher src/status_publisher.cpp)

ament_target_dependencies(status_publisher
  rclcpp
  std_msgs
)

# Link message interfaces
rosidl_target_interfaces(status_publisher
  ${PROJECT_NAME} "rosidl_typesupport_cpp"
)

# Install executable
install(TARGETS
  status_publisher
  DESTINATION lib/${PROJECT_NAME}
)

ament_package()
