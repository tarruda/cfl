cmake_minimum_required(VERSION 3.0)
project(cfl C)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# CMetrics Version
set(CFL_VERSION_MAJOR  0)
set(CFL_VERSION_MINOR  1)
set(CFL_VERSION_PATCH  0)
set(CFL_VERSION_STR    "${CTR_VERSION_MAJOR}.${CTR_VERSION_MINOR}.${CTR_VERSION_PATCH}")

# Configuration options
option(CFL_DEV             "Enable development mode"                   No)

if(CTR_DEV)
  set(CMAKE_BUILD_TYPE Debug)
endif()


add_subdirectory(src)

