add_subdirectory(unitree)

set(FORCE_BUILD_TESTS ON CACHE BOOL "Force build tests")
set(ENABLE_LOGGING ON CACHE BOOL "Enable logging")
set(ENABLE_QUADRUPED_APP ON CACHE BOOL "Enable quadruped app")
add_subdirectory(xmotion)