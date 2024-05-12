cmake_minimum_required(VERSION 3.8)
project(tdsi_moveit)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclcpp_components REQUIRED)
find_package(moveit_servo REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(control_msgs REQUIRED)
find_package(std_srvs REQUIRED)
find_package(moveit_msgs REQUIRED)

# Define a library for the component node
add_library(joy_servo_tdsi SHARED
  src/joy_servo_tdsi.cpp
)

# Register the node as a component
rclcpp_components_register_nodes(joy_servo_tdsi "tdsi_moveit::joy_servo_tdsi")

install(TARGETS
  joy_servo_tdsi
  EXPORT export_joy_servo_tdsi
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  RUNTIME DESTINATION bin
  INCLUDES DESTINATION include
)

install(DIRECTORY
  launch
  DESTINATION share/${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
