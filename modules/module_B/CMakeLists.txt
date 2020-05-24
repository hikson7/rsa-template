cmake_minimum_required(VERSION 3.14.5)
set(CMAKE_CXX_STANDARD 14)

project(module_B)

# set path for common source/header files
set(COMMON "../../common_src")
set(INCLUDE "../../common_include")

# include all files that you need for this module 
# make sure to include src files one by one
add_executable(
    ${PROJECT_NAME} 
    mainB.cpp moduleB.h      # add all the files from this module here.
    ${COMMON}/common1.cpp ${COMMON}/common2.cpp  # add all common files from the file (exclude header files)
)

# common source/header files
target_include_directories(${PROJECT_NAME} PRIVATE ${INCLUDE} ${COMMON})

# linking common source/header files
target_link_directories(${PROJECT_NAME} PRIVATE ${INCLUDE} ${COMMON})