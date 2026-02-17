# Using the same minimum as the godot-cpp project
cmake_minimum_required(VERSION 3.17)

# Silence unused variable warning when specified from toolchain
if(CMAKE_C_COMPILER)
endif()

set(LIBNAME "EXTENSION-NAME" CACHE STRING "The name of the library")
set(GODOT_PROJECT_DIR "project" CACHE STRING "The directory of a Godot project folder")

# Make sure all the dependencies are satisfied
find_package(Python3 3.4 REQUIRED)
find_program(GIT git REQUIRED)

project(${LIBNAME} LANGUAGES CXX)

add_library(${LIBNAME} SHARED)

set(MINGW_ROOT "D:/msys64/mingw64" CACHE STRING "The root of the MinGW installation")
target_include_directories(${LIBNAME} SYSTEM PUBLIC ${MINGW_ROOT}/include/godot_cpp/)

target_sources(${LIBNAME}
        PRIVATE
        src/register_types.cpp
        src/register_types.h
        src/example_class.cpp
        src/example_class.h
)

target_link_libraries(${LIBNAME} PRIVATE godot-cpp)

# Require at least C++17 for this target
set_property(TARGET ${LIBNAME} PROPERTY CXX_STANDARD 17)

string(TOLOWER "${CMAKE_SYSTEM_NAME}" GODOT_CPP_PLATFORM)
set(GODOT_PROJECT_BINARY_DIR "${PROJECT_SOURCE_DIR}/${GODOT_PROJECT_DIR}/bin/${GODOTCPP_PLATFORM}")

add_custom_command(TARGET ${LIBNAME} POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy "$<TARGET_FILE:${LIBNAME}>" "${GODOT_PROJECT_BINARY_DIR}/$<TARGET_FILE_NAME:${LIBNAME}>"
)
