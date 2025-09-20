cmake_minimum_required(VERSION 3.5)

file(GLOB LIBSCPI_SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c"
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp"
)

if(DEFINED IDF_PATH)
    idf_component_register(SRCS "${LIBSCPI_SOURCES}"
    INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/inc
    )
else()
    project(libscpi)

    add_library(libscpi ${LIBSCPI_SOURCES})

    target_include_directories(libscpi PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/inc)

    target_compile_options(libscpi PRIVATE
        -Wextra
        -Wmissing-prototypes
        -Wimplicit
        $<$<CONFIG:Release>:-fPIC>
    )

    target_link_libraries(libscpi PRIVATE m)
    target_link_options(libscpi PRIVATE -Wl,--as-needed)

    set_target_properties(libscpi PROPERTIES
        OUTPUT_NAME "scpi"
        VERSION 2.1.0
        SOVERSION 1
    )
endif()