cmake_minimum_required(VERSION 3.14.5)
set(CMAKE_CXX_STANDARD 14)

project(module_A)

# set path for common source/header files
set(COMMON "../../common_src")
set(INCLUDE "../../common_include")

# ----- EDIT HERE -----
# include all files that you need for this module 
# make sure to include src files one by one

add_executable(
    ${PROJECT_NAME} 
    mainA.cpp moduleA.h # e.g. file1.cpp file2.cpp header1.h ... 
    ${COMMON}/common1.cpp ${COMMON}/common2.cpp  # e.g. ${COMMON}/common3.cpp ...
)

# common source/header files
target_include_directories(${PROJECT_NAME} PRIVATE ${INCLUDE} ${COMMON})
# linking common source/header files
target_link_directories(${PROJECT_NAME} PRIVATE ${INCLUDE} ${COMMON})