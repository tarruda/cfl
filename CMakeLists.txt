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

# Include helpers
include(cmake/macros.cmake)
include(CheckCSourceCompiles)
include(GNUInstallDirs)

# clock_get_time() support for macOS.
check_c_source_compiles("
  #include <mach/clock.h>
  #include <mach/mach.h>
  int main() {
      clock_serv_t cclock;
      mach_timespec_t mts;
      host_get_clock_service(mach_host_self(), CALENDAR_CLOCK, &cclock);
      clock_get_time(cclock, &mts);
      return mach_port_deallocate(mach_task_self(), cclock);
  }" CFL_HAVE_CLOCK_GET_TIME)
if(CFL_HAVE_CLOCK_GET_TIME)
  CFL_DEFINITION(CFL_HAVE_CLOCK_GET_TIME)
endif()

configure_file(
  "${PROJECT_SOURCE_DIR}/include/cfl/cfl_info.h.in"
  "${PROJECT_SOURCE_DIR}/include/cfl/cfl_info.h"
  )

configure_file(
  "${PROJECT_SOURCE_DIR}/include/cfl/cfl_version.h.in"
  "${PROJECT_SOURCE_DIR}/include/cfl/cfl_version.h"
  )

# Include headers and dependency headers
include_directories(
  include
  )

add_subdirectory(src)

