cmake_minimum_required(VERSION 3.10)
project(VCFLite VERSION 0.1 LANGUAGES CXX)

set(CMAKE_BUILD_TYPE Release)
set(CMAKE_CXX_STANDARD 17)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
    set(CMAKE_INSTALL_PREFIX "/usr/local" CACHE PATH "..." FORCE)
endif()

if (NOT HEADER_INSTALL_PREFIX)
    set(HEADER_INSTALL_PREFIX "/usr/local" CACHE PATH "..." FORCE)
endif()

add_executable(TablePivot
  ${CMAKE_CURRENT_SOURCE_DIR}/src/table_pivot.cpp
)

target_include_directories(TablePivot
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/include
        ${CMAKE_CURRENT_SOURCE_DIR}/agizmo/include
)

target_compile_options(TablePivot PRIVATE
    -Werror -Wall
    -pthread -O3
    -mtune=native -march=x86-64
    -pipe -fPIE -fPIC)

install(TARGETS TablePivot RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/bin)
