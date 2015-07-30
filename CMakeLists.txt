cmake_minimum_required(VERSION 2.8.11)
cmake_policy(SET CMP0048 NEW)

# Read and set project version.
file(STRINGS ${CMAKE_CURRENT_SOURCE_DIR}/VERSION MODULE-VERSION)

# Set project name and version
project(atmine VERSION ${MODULE-VERSION})

# Fix RPATH on OS X
if(NOT DEFINED CMAKE_MACOSX_RPATH)
  set(CMAKE_MACOSX_RPATH 0)
endif()

# Fix library installation paths on certain 64 bit linux distributions
get_property(LIB64 GLOBAL PROPERTY FIND_LIBRARY_USE_LIB64_PATHS)

if(LIB64 AND (CMAKE_SYSTEM_NAME STREQUAL Linux))
  set(LIB_SUFFIX 64)
else(LIB64 AND (CMAKE_SYSTEM_NAME STREQUAL Linux))
  set(LIB_SUFFIX "")
endif(LIB64 AND (CMAKE_SYSTEM_NAME STREQUAL Linux))

set(INSTALL_LIB_DIR lib${LIB_SUFFIX} CACHE PATH "Installation directory for libraries")
mark_as_advanced(INSTALL_LIB_DIR)

# Set custom cmake modules path
set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)

# Set common compiler flags.
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wextra")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wmissing-braces")

# Add subprojects
add_subdirectory(core)
