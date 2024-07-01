add_executable(stand_go2 stand_go2.cpp)
target_link_libraries(stand_go2 PUBLIC unitree_sdk2)

add_executable(test test_unitree_sdk2.cpp)
target_link_libraries(test unitree_sdk2)
