cmake_minimum_required(VERSION 3.8)
project(segfault_node)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(backward_ros REQUIRED)

add_executable(segfault_node src/segfault_node.cpp)
target_include_directories(segfault_node PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>)
target_compile_features(segfault_node PUBLIC c_std_99 cxx_std_17)  # Require C99 and C++17
ament_target_dependencies(
  segfault_node
  "backward_ros"
)

install(TARGETS segfault_node
  DESTINATION lib/${PROJECT_NAME})

ament_package()
