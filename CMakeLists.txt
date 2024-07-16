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

if(WIN32)
    set(CMAKE_SHARED_LIBRARY_PREFIX "")
    set(CMAKE_STATIC_LIBRARY_PREFIX "")
endif()

set(LIBRARY_OUTPUT_PATH ${CMAKE_CURRENT_LIST_DIR}/bin)

add_library(optional SHARED source/optional.cpp
                                include/optional.hpp)

target_include_directories(optional PUBLIC include)
target_link_libraries(main PUBLIC optional)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_CURRENT_LIST_DIR}/bin)

