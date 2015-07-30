cmake_minimum_required(VERSION 2.8.11)
cmake_policy(SET CMP0048 NEW)

# Read and set project version.
file(STRINGS ${CMAKE_CURRENT_SOURCE_DIR}/VERSION MODULE-VERSION)

# Set project name and version
project(atmine-core VERSION ${MODULE-VERSION})

# Add source files
aux_source_directory(. SRC_LIST)

# Add header files to make Qt Creator display them too
file(GLOB HDR_LIST "*.h" "*.hpp")

# Add shared library target
add_library(${PROJECT_NAME} SHARED ${SRC_LIST} ${HDR_LIST})

# Set shared library versions
set_target_properties(${PROJECT_NAME} PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION ${PROJECT_VERSION_MAJOR}
)
