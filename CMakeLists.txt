cmake_minimum_required(VERSION 3.1.0 FATAL_ERROR)
PROJECT(halloweencontroler)

FILE(GLOB APP_SRC src/* PARENT_SCOPE)

add_subdirectory(googletest)
add_subdirectory(tests)

# only build the executable and supporting libraries when cross
# compiling.  During testing we use mocks.
if (${CMAKE_CROSSCOMPILING})
  SET(COSA_PATH Cosa/cores/cosa)
  FILE(GLOB CosaSRC ${COSA_PATH}/Cosa/*.cpp)
  SET(CosaSRC ${COSA_PATH}/main.cpp ${CosaSRC})

  add_library(cosa STATIC ${CosaSRC})
  add_executable(${project} ${APP_SRC})
  target_link_library(${project} cosa)
endif()
