cmake_minimum_required(VERSION 3.16)
project(unitree_mujoco)

find_program(CCACHE_PROGRAM ccache)

if (CCACHE_PROGRAM)
  message(STATUS "Found ccache")
  set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE "${CCACHE_PROGRAM}")
endif ()

## Generate symbols for IDE indexer
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

## Additional cmake module path
list(APPEND CMAKE_PREFIX_PATH "/opt/weston_robot/lib/cmake")

## Set compiler to use c++ 17 features
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

## Use GNUInstallDirs to install libraries into correct locations on all platforms.
include(GNUInstallDirs)

## Put all binary files into /bin and libraries into /lib
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/${CMAKE_INSTALL_BINDIR})

# Test configurations
if(PROJECT_NAME STREQUAL CMAKE_PROJECT_NAME AND BUILD_TESTING)
  enable_testing()
  include(GoogleTest)
  set(BUILD_TESTS ON)
  message(STATUS "Tests will be built")
else()
  set(BUILD_TESTS OFF)
  message(STATUS "Tests will not be built")
endif()

## Find packages
find_package(mujoco REQUIRED)
find_package(unitree_sdk2 REQUIRED)

FILE(GLOB SIM_SRC
    src/joystick/joystick.cc
    src/mujoco/*.cc
    src/unitree_sdk2_bridge/*.cc)
add_executable(unitree_mujoco ${SIM_SRC} src/main.cc)
target_link_libraries(unitree_mujoco PUBLIC
    pthread
    unitree_sdk2
    mujoco::mujoco
    glfw
    yaml-cpp)

add_executable(jstest src/joystick/jstest.cc src/joystick/joystick.cc)
target_link_libraries(jstest pthread)