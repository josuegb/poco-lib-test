set(BINARY ${CMAKE_PROJECT_NAME})

file(GLOB_RECURSE SOURCES LIST_DIRECTORIES true *.h *.cpp)

set(SOURCES ${SOURCES})

add_executable(${BINARY}_run ${SOURCES})

add_library(${BINARY}_lib STATIC ${SOURCES})


set(POCO_PREFIX "lib/poco/cmake-build/install") # the directory containing "include" and "lib"
set(POCO_INCLUDE_DIR "${POCO_PREFIX}/include")
set(POCO_LIB_DIR "${POCO_PREFIX}/lib")
set(POCO_LIBS "${POCO_LIB_DIR}/libPocoFoundation.so")



target_include_directories(${BINARY}_lib "${POCO_INCLUDE_DIR}")
target_link_libraries(${BINARY}_run "${POCO_LIBS}")