cmake_minimum_required(VERSION 3.18.4)

project(Vulkan-Minecraft)

# C++20 Version
include(cmake/c++-standards.cmake)
cxx_20()

# Formatting Commands
include(cmake/formatting.cmake)

file(GLOB_RECURSE CL_FILES *.[hc] *.[hc]pp)
list(FILTER CM_FILES EXCLUDE REGEX ${CMAKE_CURRENT_SOURCE_DIR}/build)
list(FILTER CM_FILES EXCLUDE REGEX ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
clang_format(format ${CL_FILES})

file(GLOB_RECURSE CM_FILES CMakeLists.txt *.cmake)
list(FILTER CM_FILES EXCLUDE REGEX ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
cmake_format(cmake-format ${CM_FILES})

# Dependency Graph
include(cmake/dependency-graph.cmake)
gen_dep_graph(png ADD_TO_DEP_GRAPH)

# clang-tidy

include(cmake/tools.cmake)
option(CLANG_TIDY_FIX ** OFF)
if(CLANG_TIDY_FIX)
  clang_tidy(-header-filter= '${CMAKE_SOURCE_DIR}/*' -fix)
else()
  clang_tidy(-header-filter= '${CMAKE_SOURCE_DIR}/*')
endif()

# Misc CMake
include(cmake/compiler-options.cmake)
include(cmake/sanitizers.cmake)

# Engine Entrypoint
add_executable(vulkan_minecraft)

# Sources
add_subdirectory(src)
