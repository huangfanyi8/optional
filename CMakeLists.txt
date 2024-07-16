cmake_minimum_required(VERSION 3.27)

project(optional
LANGUAGES CXX
DESCRIPTION "c++11 implement std::optional support reference type"
)

set(CMAKE_CXX_STANDARD 11)

file(GLOB test_list ${CMAKE_CURRENT_LIST_DIR}/test/*.cpp)

foreach (source_file  ${test_list})
    message("${source_file}")
endforeach ()

foreach (source_file  ${test_list})
    get_filename_component(file_name ${source_file} NAME_WE)
    message("${source_file}->${file_name}")
    add_executable(${file_name} ${source_file})
    target_include_directories(${file_name} PUBLIC ${CMAKE_CURRENT_LIST_DIR}/include)
endforeach ()

set(LIBRARY_OUTPUT_PATH ${CMAKE_CURRENT_LIST_DIR}/bin)

add_library(optional source/optional.cpp
                                include/optional.hpp)

set_target_properties(optional
                                PROPERTIES
 PREFIX "")

target_include_directories(optional PUBLIC include)

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_CURRENT_LIST_DIR}/bin)

