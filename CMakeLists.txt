cmake_minimum_required(VERSION 3.19.0)

set(MBED_PATH
    ${CMAKE_CURRENT_SOURCE_DIR}/mbed-os
    CACHE INTERNAL "")
set(MBED_CONFIG_PATH
    ${CMAKE_CURRENT_BINARY_DIR}
    CACHE INTERNAL "")

include(${MBED_PATH}/tools/cmake/app.cmake)

project(mbed_project)

add_subdirectory(${MBED_PATH})

add_executable(mbed_project)

target_include_directories(mbed_project PRIVATE
)

target_sources(mbed_project PRIVATE
  main.cpp
)

target_link_libraries(mbed_project PRIVATE
  mbed-os 
)

mbed_set_post_build(mbed_project)

option(VERBOSE_BUILD "Have a verbose build process")
if(VERBOSE_BUILD)
  set(CMAKE_VERBOSE_MAKEFILE ON)
endif()