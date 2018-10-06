# Require a recent version of cmake
cmake_minimum_required(VERSION 2.8.4 FATAL_ERROR)

# This project is C++ based.
project(your_app CXX)

if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    if (CMAKE_CXX_COMPILER_VERSION VERSION_LESS 5.0)
        message(FATAL_ERROR "GCC version must be at least 5.0!")
    endif()
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
    if (CMAKE_CXX_COMPILER_VERSION VERSION_LESS 3.5)
        message(FATAL_ERROR "Clang version must be at least 3.5!")
    endif()
else()
    message(WARNING "You are using an unsupported compiler! Compilation has only been tested with GCC >= 5.0 or Clang >= 3.5.")
endif()
    

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "../bin/")

set(CMAKE_CXX_FLAGS "-O3 -std=c++14 -pthread")

set(CMAKE_VERBOSE_MAKEFILE on)

set(example_programs
    atomicCondition
    acquireConsume
    acquireReleaseWithWaiting
    producerConsumer
    acquireReleaseFences
    acquireReleaseWithoutWaiting
    transitivity
    relaxed
    spinLockSleep
    conditionVariable
    acquireRelease
    spinLock
    fetch_mult
    spinlockAcquireRelease
   )

foreach(example_program ${example_programs})
  set(sources ${example_program}.cpp)
  source_group("Source Files" FILES{sources})

  add_executable(${example_program} ${sources})
endforeach()
    