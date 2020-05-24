# Robot software architecture template
 Template git repository for robot software architecture. Throughout the directory structure, it contains CMakeLists.txt files which are the configuration files for cmake. 

 If you're unaware of cmake, cmake is a very useful tool for building large and complicated C++ projects. With a correct setup, it will save so much of your time.

## Project Structure

```
/bin                binary files are generated here.
/build              run $make in this directory.
/common_include     add all common header files here.
/common_src         add all the common c++ files here.
/modules            add all modules here.
    /module_A
        CMakeLists.txt
    /modules_B
        CMakeLists.txt
CMakeLists.txt      root CMakeLists.txt.
```

### root project directory
This is the directory containing all project files. Along with sub-directories, it has a root CMakeLists.txt that ties all the files and cmake configurations together.
#### CMakeLists.txt (root)
```cmake
cmake_minimum_required(VERSION 3.14.5)
```
Here make sure correct cmake 
```cmake
project(my_project_name)
```
```cmake
set(CMAKE_CXX_STANDARD 14)
```
```cmake
set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/../bin)
```
```cmake
add_subdirectory(modules/Module_A)
add_subdirectory(modules/Module_B)
```
### /bin directory

### /build directory

### /common_include directory

### /common_src directory

### /module directory

## Install cmake