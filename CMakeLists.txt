cmake_minimum_required(VERSION 2.8...3.13)

project(vits-ncnn)

set(CMAKE_CXX_STANDARD 17)

add_subdirectory(ncnn)
add_subdirectory(openjtalk)
add_subdirectory(fftpack)
add_subdirectory(wave_utils)
add_subdirectory(demo)

aux_source_directory(vits vits_source)
include_directories(${CMAKE_SOURCE_DIR}/vits)

add_library(vits-ncnn SHARED ${vits_source} vitsncnn.cpp)

# 静态链接设定
set_target_properties(vits-ncnn PROPERTIES LINK_SEARCH_START_STATIC 1)
set_target_properties(vits-ncnn PROPERTIES LINK_SEARCH_END_STATIC 1)
set(CMAKE_FIND_LIBRARY_SUFFIXES ".a")

if (APPLE)
    target_link_libraries(vits-ncnn ncnn libopenjtalk libfftpack libwaveutils -static-libstdc++)
else ()
    target_link_libraries(vits-ncnn ncnn libopenjtalk libfftpack libwaveutils -static-libgcc -static-libstdc++)
endif ()