cmake_minimum_required(VERSION 3.5)
project(cpp_pubsub)

##Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(cpp_srvcli REQUIRED)

add_executable(talker src/publisher_member_function.cpp)
ament_target_dependencies(talker rclcpp std_msgs cpp_srvcli)

add_executable(listener src/subscriber_member_function.cpp)
ament_target_dependencies(listener rclcpp std_msgs cpp_srvcli)

add_executable(server src/add_two_ints_server.cpp)
ament_target_dependencies(server rclcpp cpp_srvcli)

add_executable(client src/add_two_ints_client.cpp)
ament_target_dependencies(client rclcpp cpp_srvcli)

install(TARGETS
  talker
  listener
  server
  client
  DESTINATION lib/${PROJECT_NAME})

ament_package()