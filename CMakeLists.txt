# check for minimum requirements
cmake_minimum_required(VERSION 3.14.5)
set(CMAKE_CXX_STANDARD 14)

# project(my_project_name)

# set executables output binary to /bin directory of this project file.
# (${CMAKE_BINARY_DIR} is the default binary directory for "build" directory)

set(
    CMAKE_RUNTIME_OUTPUT_DIRECTORY 
    ${CMAKE_BINARY_DIR}/../bin
)

# ----- EDIT HERE -----
# Here add directories to the build so can be referenced. List from least dependent to most dependent
add_subdirectory(modules/Module_A)
add_subdirectory(modules/Module_B)