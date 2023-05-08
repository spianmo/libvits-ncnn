cmake_minimum_required(VERSION 2.8...3.13)

project(vits-cli)

set(CMAKE_CXX_STANDARD 20)
add_executable(vits-cli vitsdemo.cpp utils.cpp)

if (APPLE)
    find_package(fmt REQUIRED)
    target_link_libraries(vits-cli ${CMAKE_SOURCE_DIR}/cmake-build-debug/libvits-ncnn.dylib fmt::fmt)
ELSEIF (WIN32)
    target_link_libraries(vits-cli ${CMAKE_SOURCE_DIR}/cmake-build-debug/libvits-ncnn.dll)
ELSE ()
    target_link_libraries(vits-cli ${CMAKE_SOURCE_DIR}/cmake-build-debug/libvits-ncnn.so)
endif ()
