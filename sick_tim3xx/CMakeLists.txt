cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

rosbuild_make_distribution(0.1.0)

rosbuild_init()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
#rosbuild_genmsg()
#uncomment if you have defined services
#rosbuild_gensrv()

#add dynamic reconfigure api
rosbuild_find_ros_package(dynamic_reconfigure)
include(${dynamic_reconfigure_PACKAGE_PATH}/cmake/cfgbuild.cmake)
gencfg()

#common commands for building c++ executables and libraries
#rosbuild_add_library(${PROJECT_NAME} src/example.cpp)
#target_link_libraries(${PROJECT_NAME} another_library)
#rosbuild_add_boost_directories()
#rosbuild_link_boost(${PROJECT_NAME} thread)
rosbuild_add_executable(sick_tim310s01 src/sick_tim310s01.cpp src/sick_tim3xx_common.cpp src/sick_tim3xx_common_usb.cpp src/sick_tim310s01_parser.cpp src/abstract_parser.cpp)
rosbuild_add_executable(sick_tim310 src/sick_tim310.cpp src/sick_tim3xx_common.cpp src/sick_tim3xx_common_usb.cpp src/sick_tim310_parser.cpp src/abstract_parser.cpp)
rosbuild_add_executable(sick_tim310_1130000m01 src/sick_tim310_1130000m01.cpp src/sick_tim3xx_common.cpp src/sick_tim3xx_common_usb.cpp src/sick_tim310_1130000m01_parser.cpp src/abstract_parser.cpp)
rosbuild_add_executable(sick_tim551_2050001 src/sick_tim551_2050001.cpp src/sick_tim3xx_common.cpp src/sick_tim3xx_common_usb.cpp src/sick_tim3xx_common_tcp.cpp src/sick_tim551_2050001_parser.cpp src/abstract_parser.cpp)
rosbuild_add_executable(sick_tim3xx_datagram_test test/sick_tim3xx_datagram_test.cpp src/sick_tim310s01_parser.cpp src/abstract_parser.cpp)

target_link_libraries(sick_tim310s01 usb-1.0)
target_link_libraries(sick_tim310 usb-1.0)
target_link_libraries(sick_tim310_1130000m01 usb-1.0)
target_link_libraries(sick_tim551_2050001 usb-1.0)
