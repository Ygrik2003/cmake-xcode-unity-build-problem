cmake_minimum_required(VERSION 3.28)
project(test CXX)

add_subdirectory(mylib)

add_library(lib_wrapper STATIC ${CMAKE_CURRENT_LIST_DIR}/lib_wrapper.cpp
                               ${CMAKE_CURRENT_LIST_DIR}/lib_wrapper.h)
target_link_libraries(lib_wrapper PRIVATE mylib)

add_executable(main ${CMAKE_CURRENT_LIST_DIR}/main.cpp)
target_link_libraries(main PRIVATE lib_wrapper)
