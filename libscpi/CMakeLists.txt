cmake_minimum_required(VERSION 3.5)
project(libscpi)

file(GLOB LIBSCPI_SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp"
)

add_library(libscpi ${LIBSCPI_SOURCES})

target_include_directories(libscpi PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/inc)

set_target_properties(libscpi PROPERTIES
    OUTPUT_NAME "scpi"
    VERSION 2.1.0
    SOVERSION 1
)