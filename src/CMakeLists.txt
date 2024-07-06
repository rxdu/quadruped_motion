add_subdirectory(unitree)

set(FORCE_BUILD_TESTS ON CACHE BOOL "Force build tests")
set(ENABLE_QUADRUPED_APP ON CACHE BOOL "Enable quadruped app")
add_subdirectory(xmotion)