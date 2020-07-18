
cmake_minimum_required(VERSION 3.10)

project(cudd)
#set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

#set(CMAKE_CXX_STANDARD 11)
#set(CMAKE_CXX_STANDARD_REQUIRED True)

#find_package(Boolector REQUIRED)
#enable_testing()

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_FLAGS "-Wall -Wextra")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")

set(CMAKE_CXX_FLAGS_DEBUG "-O3 -g")

file (GLOB_RECURSE libcudd_SRC
    "cudd/*.h"
    "cudd/*.c"
    "util/*.h"
    "util/*.c"
    )
    
CHECK_INCLUDE_FILE("assert.h", HAVE_ASSERT_H)
    
configure_file("${PROJECT_SOURCE_DIR}/config.h.in"
               "${PROJECT_BINARY_DIR}/config.h")

add_library(cudd SHARED ${libcudd_SRC})

target_include_directories(cudd PUBLIC
    "${PROJECT_SOURCE_DIR}/util"
    "${PROJECT_SOURCE_DIR}/cudd"
    "${PROJECT_BINARY_DIR}"
    )

