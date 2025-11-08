cmake_minimum_required(VERSION 3.8)
project(build_test)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)

# Add executable
add_executable(test_node src/test_node.cpp)

# Install targets
install(TARGETS
  test_node
  DESTINATION lib/${PROJECT_NAME})

if(BUILD_TESTING)
  # Manually specify only the linters we want to use
  find_package(ament_cmake_cppcheck REQUIRED)
  find_package(ament_cmake_lint_cmake REQUIRED)
  find_package(ament_cmake_flake8 REQUIRED)
  find_package(ament_cmake_pep257 REQUIRED)
  find_package(ament_cmake_uncrustify REQUIRED)
  find_package(ament_cmake_xmllint REQUIRED)

  ament_cppcheck()
  ament_lint_cmake()
  ament_flake8()
  ament_pep257()
  ament_uncrustify()
  ament_xmllint()

  # simple gtest
  find_package(ament_cmake_gtest REQUIRED)
  ament_add_gtest(${PROJECT_NAME}_tutorial_test test/tutorial_test.cpp)
  target_include_directories(${PROJECT_NAME}_tutorial_test PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
  )
endif()

ament_package()
