cmake_minimum_required(VERSION 3.5)

project(osrf_testing_tools_cpp)

set(osrf_testing_tools_cpp_VERSION 1.5.1)

# Default to C++11
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 11)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic
  -Wformat=2 -Wconversion -Woverloaded-virtual
  -Wshadow -Wnon-virtual-dtor)
endif()

if (EMSCRIPTEN)
  set(CMAKE_CXX_FLAGS "-pthread ${CMAKE_CXX_FLAGS}")
endif()

add_subdirectory(src)

configure_file(osrf_testing_tools_cppConfig.cmake.in
  "${PROJECT_BINARY_DIR}/osrf_testing_tools_cppConfig.cmake" @ONLY)
configure_file(osrf_testing_tools_cppConfigVersion.cmake.in
  "${PROJECT_BINARY_DIR}/osrf_testing_tools_cppConfigVersion.cmake" @ONLY)

install(FILES
  "${PROJECT_BINARY_DIR}/osrf_testing_tools_cppConfig.cmake"
  "${PROJECT_BINARY_DIR}/osrf_testing_tools_cppConfigVersion.cmake"
  DESTINATION share/${PROJECT_NAME}/cmake
)

install(DIRECTORY vendor/
  DESTINATION share/${PROJECT_NAME}/vendor
  PATTERN ".gitattributes" EXCLUDE
)

install(DIRECTORY cmake/
  DESTINATION share/${PROJECT_NAME}/cmake
)

install(
  DIRECTORY include/
  DESTINATION include
)

install(FILES
  package.xml
  DESTINATION share/${PROJECT_NAME})
