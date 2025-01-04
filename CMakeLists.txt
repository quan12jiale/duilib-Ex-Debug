# CMake root file for duilib related apps
#Date 2012-09-16
#Author: Qi Gao(monkgau@gmail.com)
#
#  CMake files for duilib
#  file for each app is under the related sub-dir
#

cmake_minimum_required(VERSION 3.13)

project(dui)

# 设置一个变量
set(DUILIB_BUILD_EXAMPLES TRUE) # TRUE FALSE
#option(DUILIB_BUILD_EXAMPLES "Build examples" ON)

message(STATUS," CMake project files for duilib")

# this line is for UNICODE release,which is required by DuiDesigner 
add_definitions(-DUNICODE -D_UNICODE)

##源代码位置
set(PROJECT_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/")

##将动态库\静态库输出路径定位到特定路径,供调试时使用(否则依赖的库分布在各个文件夹)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}bin")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}build/lib/${PROJECT_PLATFORM}/$<CONFIG>")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}build/lib/${PROJECT_PLATFORM}/$<CONFIG>")

# add each CMake file
add_subdirectory(duilib)

if (DUILIB_BUILD_EXAMPLES)
    add_subdirectory(DuiDesigner)
endif()

# 设置启动项
set_property(DIRECTORY PROPERTY VS_STARTUP_PROJECT DuiDesigner)

install(FILES ${PROJECT_SOURCE_DIR}/LICENSE DESTINATION share/${PROJECT_NAME})
