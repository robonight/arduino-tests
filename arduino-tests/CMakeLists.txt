cmake_minimum_required (VERSION 2.8.8)
project (arduino_mock)

find_package(Threads REQUIRED)
add_subdirectory(mock/lib/gtest)
add_subdirectory(mock/lib/gmock)

message ("=================== building arduino_mock")
message("Gtest include: ${GTEST_INCLUDE_DIRS}")
message("Gmock include: ${GMOCK_INCLUDE_DIRS}")
include_directories(${GTEST_INCLUDE_DIRS} ${GMOCK_INCLUDE_DIRS} include)
file(GLOB SRC
    "mock/src/ArduinoMockAll.cc"
)


message ("=================== adding libraries for aduino mocks")
add_library(arduino_mock STATIC ${SRC})

target_include_directories(arduino_mock
    PUBLIC "mock/include"
)

target_link_libraries(arduino_mock
    ${GTEST_LIBS_DIR}/libgtest.a
    ${GMOCK_LIBS_DIR}/libgmock.a
    ${CMAKE_THREAD_LIBS_INIT}
)

set_target_properties( arduino_mock
  PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "mock/dist/lib"
    LIBRARY_OUTPUT_DIRECTORY "mock/dist/lib"
    RUNTIME_OUTPUT_DIRECTORY "mock/dist/bin"
)

add_dependencies(arduino_mock gtest gmock)

option(test "Build all tests." OFF)

if (test)
  enable_testing()
  add_subdirectory(project/test)

  message ("=================== building tests for Arduino Mock")
  include_directories(${GTEST_INCLUDE_DIRS})
  file(GLOB SRCS **/*.cc)

  add_executable(test_all project/test/test_all.cc)

  target_link_libraries(test_all
      arduino_mock
      ${GTEST_LIBS_DIR}/libgtest.a
      ${GTEST_LIBS_DIR}/libgtest_main.a
      ${GMOCK_LIBS_DIR}/libgmock.a
      ${CMAKE_THREAD_LIBS_INIT}
  )

  add_dependencies(test_all gtest)
  add_test(arduino_mock_test test_all)
endif()