cmake_minimum_required(VERSION 3.0.0)
project(codecov-example VERSION 0.0.0)

include(CTest)
enable_testing()

add_executable(codecov-example main.cpp)
add_executable(test1 test.cpp)

add_test(test1 test1)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
