cmake_minimum_required(VERSION 3.4.1)

set(CMAKE_VERBOSE_MAKEFILE on)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
add_library(lib_so SHARED src/two.c)

set(distribution_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../../../../libBuild)
set_target_properties(lib_so
                      PROPERTIES
                      LIBRARY_OUTPUT_DIRECTORY
                      "${distribution_DIR}/two/lib/${ANDROID_ABI}")
add_custom_command(TARGET lib_so POST_BUILD
                   COMMAND "${CMAKE_COMMAND}" -E
                   copy "${CMAKE_CURRENT_SOURCE_DIR}/include/two.h"
                   "${distribution_DIR}/two/include/two.h"
                   COMMENT "Copying two to output directory")