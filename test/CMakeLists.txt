include_directories(SYSTEM 
    ${CMAKE_SOURCE_DIR}/googletest/googlemock/include)

enable_testing()

FILE(GLOB TEST_SRC *.cpp)

SET(TEST_NAME ${PROJECT_NAME}-test)

ADD_EXECUTABLE(${TEST_NAME}
    ${TEST_SRC}
    ${APP_SRC}
    )

SET_PROPERTY(TARGET ${TEST_NAME} PROPERTY CXX_STANDARD 14)
TARGET_LINK_LIBRARIES(${TEST_NAME}
	gmock
	gtest
	gtest_main)

TARGET_COMPILE_FEATURES(${TEST_NAME} PUBLIC cxx_override)
ADD_TEST(UnitTest ${TEST_NAME})