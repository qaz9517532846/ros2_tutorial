cmake_minimum_required(VERSION 3.5)

project(tlsf_cpp)
if(WIN32 OR APPLE OR ANDROID)
  message(STATUS "tlsf allocator does not target Windows, OSX or Android, skipping...")
  return()
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(tlsf REQUIRED)

include_directories(include)

add_executable(tlsf_cpp src/tlsf_cpp.cpp)
ament_target_dependencies(tlsf_cpp "rclcpp" "std_msgs" "tlsf")
  
install(TARGETS 
  tlsf_cpp
  DESTINATION lib/${PROJECT_NAME})

ament_export_include_directories(include)
ament_export_dependencies("tlsf")

install(DIRECTORY include/
  DESTINATION include)
  
ament_package()
