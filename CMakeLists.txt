cmake_minimum_required(VERSION "3.0.0")

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib")

set(VALID_BUILD_TYPES "Release" "Debug" "MinSizeRel" "RelWithDebInfo")

option(BUILD_SHARED_LIBS "True when building a shared library" True)

project("CMakeTests")

if(NOT CMAKE_CONFIGURATION_TYPES)
    if("${CMAKE_BUILD_TYPE}" STREQUAL "")
        set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Build configuration" FORCE)
    endif()
endif()

if(NOT CMAKE_CONFIGURATION_TYPES)
    list(FIND VALID_BUILD_TYPES "${CMAKE_BUILD_TYPE}" INDEX)
    if(${INDEX} MATCHES -1)
        message(FATAL_ERROR "Invalid build type. Valid types are [${VALID_BUILD_TYPES}]")
    endif()
endif()

if(NOT CMAKE_CONFIGURATION_TYPES)
    if(DEFINED CMAKE_BUILD_TYPE)
        set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS ${VALID_BUILD_TYPES})
    endif()
endif()

add_subdirectory("CMakeTests")
add_subdirectory("example")

include(CTest)
include(CPack)

add_test("Test1" "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}")

