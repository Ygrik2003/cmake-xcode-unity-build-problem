cmake_minimum_required(VERSION 3.28)

add_library(mylib OBJECT ${CMAKE_CURRENT_LIST_DIR}/mylib.cpp
                         ${CMAKE_CURRENT_LIST_DIR}/mylib.h)
target_include_directories(mylib PUBLIC ${CMAKE_CURRENT_LIST_DIR})
