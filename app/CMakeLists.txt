cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_VERBOSE_MAKEFILE on)

#lib_src_DIR设置路径(全局变量) 指向环境变量HOME/tmp(临时)目录
set(lib_src_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src/main/cpp)
set(lib_build_DIR $ENV{HOME}/tmp)

#创建lib_build_DIR目录(打包临时目录)
file(MAKE_DIRECTORY ${lib_build_DIR})

#add_subdirectory构建添加一个子路径。子路径中的 CMakeLists.txt 也会被执行
#add_subdirectory(${lib_src_DIR}/one ${lib_build_DIR}/one)
add_subdirectory(${lib_src_DIR}/two ${lib_build_DIR}/two)