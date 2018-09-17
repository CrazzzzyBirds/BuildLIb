cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_VERBOSE_MAKEFILE on)


#指定用到的系统库或者NDK库或者第三方库的搜索路径。
#link_directories(../lib)

#头文件引用路径
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

#编译出一个静态库 源文件是 src/main/cpp/one/src/one.c
add_library( # Sets the name of the library.
             lib_a
             # Sets the library as a shared library.
             STATIC
             # Provides a relative path to your source file(s).
             ${CMAKE_CURRENT_SOURCE_DIR}/src/one.c )

# 设置库文件存放路径
set(lib_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../../../../libBuild)

set_target_properties(lib_a
                      PROPERTIES
                      ARCHIVE_OUTPUT_DIRECTORY
                      "${lib_DIR}/one/lib/${ANDROID_ABI}")

# copy out lib header file... TARGET 库名 POST_BUILD
add_custom_command(TARGET lib_a POST_BUILD
                   COMMAND "${CMAKE_COMMAND}" -E
                    #复制路径（头文件地址）
                   copy "${CMAKE_CURRENT_SOURCE_DIR}/include/one.h"
                    #目标路径
                   "${lib_DIR}/one/include/one.h"
                   COMMENT "Copying one to output directory")
