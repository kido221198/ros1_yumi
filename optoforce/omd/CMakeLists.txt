cmake_minimum_required (VERSION 2.6)
project(omd)

message ("********************************************")
message ("starting cmake management of ${PROJECT_NAME}")
include_directories(include)
find_library(LIBOMD NAMES "OMD" PATHS "${CMAKE_CURRENT_LIST_DIR}/lib/linux")

# Compatiblity with ROS
if(DEFINED ENV{ROS_ROOT})
  message ("ROS defined -- using catkin ")
  find_package(catkin REQUIRED)
  catkin_package(INCLUDE_DIRS include
    LIBRARIES ${LIBOMD})
else()
  message ("ROS not defined -- not using catkin ")
endif()


list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake")
# this line was uncommented.
#find_package(omd)

# Would have thought this solution would be enough .. to be investigated
#message("omd path defined ${CMAKE_CURRENT_LIST_DIR}")
#set(omd_LIBRARIES "${CMAKE_CURRENT_LIST_DIR}/lib/linux/libOMD.so")
#set(omd_INCLUDE_DIRS "${CMAKE_CURRENT_LIST_DIR}/include")
# Define headers for this library. PUBLIC headers are used for
# compiling the library, and will be added to consumers' build
# paths.

# target_include_directories(omd PUBLIC
#     $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
#     $<INSTALL_INTERFACE:include>
#     PRIVATE src)

# install(TARGETS omd
#     ARCHIVE  DESTINATION lib
#     LIBRARY  DESTINATION lib
#     RUNTIME  DESTINATION bin)  # This is for Windows
# install(DIRECTORY include/ DESTINATION include)

# # This makes the project importable from the build directory
# export(TARGETS omd FILE omdConfig.cmake)

if(DEFINED ENV{ROS_ROOT})
  install(DIRECTORY include/${PROJECT_NAME}/
    DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
    FILES_MATCHING PATTERN "*.h"
    PATTERN ".svn" EXCLUDE
  )
  install(PROGRAMS ${LIBOMD}
    DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  )
endif()

message ("********************************************")
message ("cmake management of ${PROJECT_NAME} done")
