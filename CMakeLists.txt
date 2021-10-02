cmake_minimum_required(VERSION 3.18.4)

project(Vulkan-Minecraft)

# C++20 Version
include(cmake/c++-standards.cmake)
cxx_20()

# Formatting Commands
include(cmake/formatting.cmake)

##file(GLOB_RECURSE CL_FILES src/*.[hc] src/*.[hc]pp)
##clang_format(format ${CL_FILES})

##file(GLOB_RECURSE CM_FILES CMakeLists.txt *.cmake)
##cmake_format(cmake-format ${CM_FILES})

# Engine Entrypoint
add_executable(vulkan_minecraft)

add_subdirectory(src)