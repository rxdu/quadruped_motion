## Find packages
find_package(mujoco REQUIRED)
find_package(unitree_sdk2 REQUIRED)

FILE(GLOB SIM_SRC
    joystick/joystick.cc
    mujoco/*.cc
    unitree_sdk2_bridge/*.cc)
add_executable(unitree_mujoco ${SIM_SRC} main.cc)
target_link_libraries(unitree_mujoco PUBLIC
    pthread
    unitree_sdk2
    mujoco::mujoco
    glfw
    yaml-cpp)

add_executable(jstest joystick/jstest.cc joystick/joystick.cc)
target_link_libraries(jstest pthread)

add_subdirectory(test)