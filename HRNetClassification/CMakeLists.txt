cmake_minimum_required(VERSION 2.6)

project(hrnet)

add_definitions(-std=c++11)

option(CUDA_USE_STATIC_CUDA_RUNTIME OFF)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Debug)

find_package(CUDA REQUIRED)

set(CUDA_NVCC_PLAGS ${CUDA_NVCC_PLAGS};-std=c++11;-g;-G;-gencode;arch=compute_30;code=sm_30)

include_directories(${PROJECT_SOURCE_DIR}/include)

find_package(OpenCV)
include_directories(OpenCV_INCLUDE_DIRS)

add_executable(hrnet ${PROJECT_SOURCE_DIR}/hrnet.cpp)
target_link_libraries(hrnet nvinfer)
target_link_libraries(hrnet cudart)
target_link_libraries(hrnet ${OpenCV_LIBS})

add_definitions(-O2 -pthread)

