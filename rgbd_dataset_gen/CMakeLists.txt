cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)

rosbuild_init()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

find_package(OpenCV REQUIRED)

rosbuild_add_boost_directories()

#----
rosbuild_add_executable(record
src/record_node.cpp
src/record_bagfile.cpp)

target_link_libraries(record ${OpenCV_LIBS})

#----
rosbuild_add_executable (apply_blur_noise 
src/apply_blur_noise.cpp
)
target_link_libraries(apply_blur_noise ${OpenCV_LIBS})

#----
rosbuild_add_executable (create_dataset
src/create_dataset.cpp
)
target_link_libraries(create_dataset ${OpenCV_LIBS})

