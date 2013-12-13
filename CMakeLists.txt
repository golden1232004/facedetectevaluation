cmake_minimum_required(VERSION 2.8)

project(face_detect_evaluation)

if (CMAKE_COMPILER_IS_GNUC OR CMAKE_COMPILER_IS_GNUCXX)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC")
endif ()

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)

include_directories(/usr/local/include/opencv/)   #include "cv.h", "highgui.h"

find_library(opencv_core_Lib NAMES opencv_core)
find_library(opencv_highgui_Lib opencv_highgui)

include_directories(./include/)
file(GLOB lib_srcs ./src/*.cpp ./src/*.c)
set(targetLib fd_evaluation)                    #set lib name
add_library(${targetLib} SHARED ${lib_srcs})
add_executable(evaluate_example ./systest/evaluate.cpp)
target_link_libraries(evaluate_example ${targetLib} ${opencv_core_Lib} ${opencv_highgui_Lib})