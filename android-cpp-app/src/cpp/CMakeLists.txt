cmake_minimum_required(VERSION 3.10)

project(android_native)

# compile android glue code
set(${CMAKE_C_FLAGS}, "${CMAKE_C_FLAGS}")
add_library(native_app_glue STATIC ${ANDROID_NDK}/sources/android/native_app_glue/android_native_app_glue.c)

# compile main app
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11 -Wall -Werror")
set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -u ANativeActivity_onCreate")
add_library(android_native main.cpp)


# include directories
target_include_directories(android_native PRIVATE ${ANDROID_NDK}/sources/android/native_app_glue)


# add lib dependencies
target_link_libraries(android_native android native_app_glue)