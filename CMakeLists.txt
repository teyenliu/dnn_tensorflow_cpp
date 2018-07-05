cmake_minimum_required(VERSION 3.0 FATAL_ERROR)

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)
# Instruct CMake to run moc automatically when needed
set(CMAKE_AUTOMOC ON)
# Create code from a list of Qt designer ui files
set(CMAKE_AUTOUIC ON)

project(DNN_Tensorflow_CPP LANGUAGES CXX)

add_executable(${PROJECT_NAME} model.cc data_set.cc data_set.h)
#target_link_libraries(main PRIVATE tensorflow)

configure_file(normalized_car_features.csv ${CMAKE_CURRENT_BINARY_DIR}/normalized_car_features.csv COPYONLY)
if(MSVC)
    target_compile_definitions(main PRIVATE COMPILER_MSVC)
endif(MSVC)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -g -fPIC  ")
set(CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} " )

include_directories("/usr/local/tensorflow/include/external/nsync/public")
include_directories("/usr/local/tensorflow/include/")

TARGET_LINK_LIBRARIES(${PROJECT_NAME}  "/usr/local/tensorflow/lib/libtensorflow_cc.so")
TARGET_LINK_LIBRARIES(${PROJECT_NAME}  "/usr/local/tensorflow/lib/libtensorflow_framework.so")
