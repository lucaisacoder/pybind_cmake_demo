cmake_minimum_required(VERSION 3.2 FATAL_ERROR)
project(demo LANGUAGES CXX C)

# -------- CONFIGURATION --------
# Set module name here. MUST MATCH the module name specified in the .cpp
set(PY_MODULE_NAME demo)
# Set C++11 as standard for the whole project
set(CMAKE_CXX_STANDARD 11)
# pybind11 defaults to c++14.
set(PYBIND11_CPP_STANDARD -std=c++11)

set(PYBIND11_DIR /opt/pybind11/)
set(PYTHON_ROOT /usr/include)

find_path(_PYTHON3_INC_DIR Python.h HINTS ${PYTHON_ROOT} PATH_SUFFIXES python3.7 python3.6 python3.5 python3.4)
set(PYTHON3_INC_DIR ${_PYTHON3_INC_DIR})

# Add include directories
include_directories(${PYBIND11_DIR}/include/)

# Add this so we can retrieve pybind11_add_module.
add_subdirectory(${PYBIND11_DIR} ${CMAKE_BINARY_DIR}/pybind11)

file(GLOB_RECURSE SOURCE_FILES ${CMAKE_SOURCE_DIR}/plugin/*.cpp)

pybind11_add_module(${PY_MODULE_NAME} SHARED THIN_LTO ${SOURCE_FILES})
target_include_directories(${PY_MODULE_NAME} BEFORE PUBLIC ${PYTHON3_INC_DIR})
target_link_libraries(${PY_MODULE_NAME})
