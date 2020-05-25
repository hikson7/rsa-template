# Robot software architecture template
 Template git repository for robot software architecture. Throughout the directory structure, it contains CMakeLists.txt files which are the configuration files for cmake. 

 If you're unaware of cmake, cmake is a very useful tool for building large and complicated C++ projects. With the correct setup, it will save much of your time.

## Project Structure

```
/your_project_name      this is your project root directory
    /bin                binary files are generated here.
    /build              run $make in this directory.
    /common_include     add all common header files here.
    /common_src         add all the common c++ files here.
    /modules            add all modules here.
        /module_A
            ...         module A files
            CMakeLists.txt  cmake config for module A.
        /modules_B
            ...         module B files
            CMakeLists.txt  cmake config for module B.
    CMakeLists.txt          root cmake config.
```

### root project directory
This is the directory containing all project files. Along with sub-directories, it has a root CMakeLists.txt that ties all the files and cmake configurations together.
#### CMakeLists.txt (root)

Firstly, check for cmake requirements.
```cmake
cmake_minimum_required(VERSION 3.14.5)
set(CMAKE_CXX_STANDARD 14)
```
Then, set where the executables will be produced (In our case, they will be produced in /bin directory). This is not necessary, although it keeps the code clean.

The default location for executables (${CMAKE_BINARY_DIR}) is where you run cmake i.e. /build directory.
```cmake
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY 
    ${CMAKE_BINARY_DIR}/../bin          #change this directory if desired
)
```

Finally, following makes sure to look for cmake configurations for each modules. Don't forget to add more subdirectories as you add more modules (i.e. directories that contain your module files).
```cmake
add_subdirectory(modules/Module_A)
add_subdirectory(modules/Module_B)
```
### /bin directory

This is the directory where all the executables are located after running make.

### /build directory

This is the directory that will contain build files for cmake. It is currently empty, but as you run $cmake -B build/, cmake will produce CMakeCache.txt and bunch of other configuration files necessary for cmake.

You will find the Makefile necessary to compile your project in this directory. You would only need to run cmake once to build the necessary build files, however if you change the location of this project file, you may have to delete the CMakeCache.txt and re-build the build files using cmake.

### /common_include directory

Place common header files i.e. .h files that will be shared between different modules.

### /common_src directory

Place common source files i.e. .cpp files that will be shared between different modules.

### /module directory

Place your modules here. I define module as a set of files that together create an executable. For example, if you want a program for processing/communicating data from a LIDAR, then you would place all the related files in a LIDAR module directory.

#### CMakeLists.txt (module)
Set ${PROJECT_NAME} for this module.
```cmake
project(module_A)
```
Include paths for common source/header files.
```cmake
set(COMMON "../../common_src")
set(INCLUDE "../../common_include")
```
```cmake
add_executable(
    ${PROJECT_NAME}
```
Here, include all files that is contained within the module subdirectory.
If you create new files for your module, make sure to add them in this line.
```cmake
    mainA.cpp moduleA.h # e.g. file1.cpp file2.cpp header1.h ... 
```
If you want to include any files that are common across different modules, place them inside /common_include and /common_src directories, and add the source files in this line. Don't forget to add ${COMMON}/ before the file name.
```cmake
    ${COMMON}/common1.cpp ${COMMON}/common2.cpp  # e.g. ${COMMON}/common3.cpp ...
)
```

Following line adds given paths to look for necessary files when compiling.
```cmake
target_include_directories(${PROJECT_NAME} PRIVATE ${INCLUDE} ${COMMON})
```
Following line adds given paths for linking necessary files.
```cmake
target_link_directories(${PROJECT_NAME} PRIVATE ${INCLUDE} ${COMMON})
```

## Building the project

0. make sure you have the correct cmake requirements. Install correct cmake version as necessary. 
1. go to project root directory. 
    ```
    $cd your_project_name
    ```
2. run:
    ```
    $cmake -B build/
    ```
    This creates CMakeCache.txt and other cmake build configuration files. You would only need to run this once.
3. Go to /build directory.
    ```
    $cd build
    ```
4. run:
    ```
    $make
    ```
    This will create executable associated to each module. Run this command every time you make changes in your code and need to re build your executables. 

If you've successfully built the code contained in the repo, you would see two executables in /bin directory: module_A and module_B. If you run the executables, it should produce following output.

```
$ ./bin/module_A
Hello from foo_common1()
G'day from foo_common2()
Bonjour from foo1_A()
Ciao from foo2_A()
```

```
$ ./bin/module_B
Hello from foo_common1()
G'day from foo_common2()
Ni hao from foo1_B()
Shalom from foo2_B()
```
## Install cmake
### Linux
```
$ cd Downloads
$ tar zxf cmake-3.17.2.tar.gz
$ cd cmake-3.17.2
$ sudo ./bootstrap
($ sudo apt install libssl-dev)
$ sudo make
$ sudo make install
$ cmake --version

```
