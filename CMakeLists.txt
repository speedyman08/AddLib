cmake_minimum_required(VERSION 3.31)
project(AddLib
    DESCRIPTION "Implements an Adder class, with the Add method"
    LANGUAGES CXX
    VERSION 0.0.1
)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_INSTALL_PREFIX ${CMAKE_CURRENT_SOURCE_DIR}/staging)

add_library(AddLib
        src/Add.cpp
        include/Add.h)
target_include_directories(AddLib PRIVATE include/)

# Install into staging/
install(TARGETS AddLib
    EXPORT AddClass
    LIBRARY DESTINATION lib
)

install(DIRECTORY include/
        DESTINATION include
)

install(EXPORT AddClass
        FILE AddLibTargets.cmake
        NAMESPACE AddLib::
        DESTINATION lib/cmake/
)

# Generate config file
include(CMakePackageConfigHelpers)
configure_package_config_file(
        ${CMAKE_CURRENT_SOURCE_DIR}/cmake/AddLibConfig.cmake.in
        ${CMAKE_CURRENT_SOURCE_DIR}/cmake/AddLibConfig.cmake
        INSTALL_DESTINATION lib/cmake
)