cmake_minimum_required(VERSION 3.10)

if(${CMAKE_VERSION} VERSION_LESS 3.15)
  cmake_policy(VERSION ${CMAKE_MAJOR_VERSION}.${CMAKE_MINOR_VERSION})
else()
  cmake_policy(VERSION 3.15)
endif()

include_guard(GLOBAL)

project(hjson
  VERSION 1.4
  DESCRIPTION "Human readable JSON"
  LANGUAGES CXX)

option(BUILD_SHARED_LIBS "Build shared libraries" OFF)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

set(json_src
  src/hjson_decode.cpp
  src/hjson_encode.cpp
  src/hjson_parsenumber.cpp
  src/hjson_value.cpp
)

add_library(hjson STATIC ${json_src})

target_include_directories(hjson PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include/hjson)
target_compile_options(hjson PRIVATE -Wno-sign-compare -Wno-implicit-fallthrough
                                     -Wno-covered-switch-default -Wno-unreachable-code-return)
set_target_properties(hjson PROPERTIES
  VERSION ${PROJECT_VERSION}
  SOVERSION ${PROJECT_VERSION_MAJOR}
)
