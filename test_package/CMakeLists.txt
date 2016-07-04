PROJECT(PackageTest)
cmake_minimum_required(VERSION 2.8.12)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

if(NOT MSVC)
    set(CMAKE_CXX_FLAGS "-Wall -Werror -g -Wextra -Wshadow -pedantic ${CMAKE_CXX_FLAGS}")
    if(CMAKE_VERSION VERSION_LESS 3.1)
        set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")
    else()
        if(NOT DEFINED CMAKE_CXX_STANDARD OR CMAKE_CXX_STANDARD STREQUAL "98")
            set(CMAKE_CXX_STANDARD 11)
        endif()
        set(CMAKE_CXX_STANDARD_REQUIRED ON)
    endif()
endif()

# This executable comes from a test in the GLM repo.
ADD_EXECUTABLE(example example.cpp)
TARGET_LINK_LIBRARIES(example ${CONAN_LIBS})
