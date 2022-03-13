cmake_minimum_required(VERSION 2.6)

project(yolox)

add_definitions(-std=c++11)

option(CUDA_USE_STATIC_CUDA_RUNTIME OFF)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Debug)
cmake_policy(SET CMP0060 NEW)

find_package(CUDA REQUIRED)

include_directories(${PROJECT_SOURCE_DIR}/include)
# include and link dirs of cuda and tensorrt, you need adapt them if yours are different
# cuda
include_directories(/usr/local/targets/aarch64-linux/include)
link_directories(/usr/local/targets/aarch64-linux/lib)
include_directories(/usr/local/cuda-10.2/targets/aarch64-linux/include)
link_directories(/usr/local/cuda-10.2/targets/aarch64-linux/lib)
# cudnn
include_directories(/usr/local/targets/aarch64-linux/include)
link_directories(/usr/local/targets/aarch64-linux/lib)
# tensorrt
include_directories(/usr/local/targets/aarch64-linux/include)
link_directories(/usr/local/targets/aarch64-linux/lib)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -Ofast -Wfatal-errors -D_MWAITXINTRIN_H_INCLUDED")

find_package(OpenCV)
include_directories(${OpenCV_INCLUDE_DIRS})

add_executable(yolox ${PROJECT_SOURCE_DIR}/yolox.cpp)
target_link_libraries(yolox nvinfer)
target_link_libraries(yolox cudart)
target_link_libraries(yolox ${OpenCV_LIBS})

add_definitions(-O2 -pthread)

