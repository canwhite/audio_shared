cmake_minimum_required(VERSION 3.10)

set(APP_NAME "audio")

project(${APP_NAME})

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED True)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_C_COMPILER "/opt/homebrew/opt/llvm/bin/clang")
set(CMAKE_CXX_COMPILER "/opt/homebrew/opt/llvm/bin/clang++")

find_package(PkgConfig REQUIRED)

pkg_check_modules(FFMPEG REQUIRED IMPORTED_TARGET libavformat libavcodec libavutil libswscale libavfilter libswresample) 

set(SOURCE_FILES get_audio.cpp)


# 注意引入
# add_executable(${APP_NAME} ${SOURCE_FILES} )
add_library(${APP_NAME} ${SOURCE_FILES})

#生成动态库
# set(BUILD_SHARED_LIBS TURE)
# set(SOURCE_FILES utils.c)



target_link_libraries(${APP_NAME} PkgConfig::FFMPEG)



# ##### 引入静态库
# add_library(libmp3lame STATIC IMPORTED)
# # 设置包属性，指明.a文件导入的路径
# set_target_properties(libmp3lame PROPERTIES
#     IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/libs/lame_static/lib/libmp3lame.a
# )
# #  引入字典目录，.h文件，方便主文件引用
# target_include_directories(${APP_NAME} PRIVATE ${CMAKE_SOURCE_DIR}/libs/lame_static/include/lame)
# #  项目link
# target_link_libraries(${APP_NAME}  libmp3lame)
