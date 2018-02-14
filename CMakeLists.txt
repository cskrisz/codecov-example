cmake_minimum_required(VERSION 3.0.0)
project(codecov-example VERSION 0.0.0)

set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/CMakeModules)

include(CodeCoverage)
set(CMAKE_CXX_FLAGS "-g -O0 -fprofile-arcs -ftest-coverage")
setup_target_for_coverage(my_coverage_target ./test_driver.sh coverage)

include(CTest)
enable_testing()

add_executable(codecov-example main.cpp)
add_executable(test1 test.cpp)

add_custom_command(
        TARGET codecov-example POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy
                ${CMAKE_SOURCE_DIR}/test_driver.sh
                ${CMAKE_CURRENT_BINARY_DIR})

add_test(NAME test1 COMMAND test1)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
