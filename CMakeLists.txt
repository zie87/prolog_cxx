cmake_minimum_required(VERSION 3.1)

project(prolog_cxx LANGUAGES C CXX VERSION 0.0.1)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/cmake")

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(PROJECT_TEST_NAME "${PROJECT_NAME}_test")
if (CMAKE_BUILD_TYPE STREQUAL "Coverage")
  include(CodeCoverage)
  set(CMAKE_CXX_FLAGS "-g -O0 -Wall --coverage")
  set(LCOV_REMOVE_EXTRA 'test/*' '3rd/*')
  setup_target_for_coverage(test_coverage ${PROJECT_TEST_NAME} coverage)
endif (CMAKE_BUILD_TYPE STREQUAL "Coverage")


add_subdirectory (3rd EXCLUDE_FROM_ALL)

include_directories(inc)
add_subdirectory(test)
add_subdirectory(example)

find_package(Doxygen)
if(DOXYGEN_FOUND)
    add_subdirectory(doc)
endif()

include(CTest)
enable_testing()