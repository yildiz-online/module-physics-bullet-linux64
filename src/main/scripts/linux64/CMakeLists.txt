cmake_minimum_required (VERSION 3.0.0)

project (yildiz_native_bullet)

set(CMAKE_CXX_FLAGS "-O2 -fPIC -std=gnu++11")

include_directories("bullet/linux64/include/bullet")
include_directories("java/include")
include_directories("java/include/linux")

file(
        GLOB_RECURSE
        source_files
        ${CMAKE_SOURCE_DIR}/../../includes/*.h
        ${CMAKE_SOURCE_DIR}/../../includes/*.hpp
        ${CMAKE_SOURCE_DIR}/../../c++/*.cpp

)

add_library(yildizbullet SHARED ${source_files})
target_link_libraries(yildizbullet ${BULLET_LIBRARIES})

option(BUILD_TESTS "Determines whether to build tests." OFF)
if(GB_BUILD_TESTS)
  add_executable(yildizbullet_test ${source_files})
  target_link_libraries(yildizbullet_test ${BULLET_LIBRARIES})
  enable_testing()
  add_test(NAME yildizbullet_test COMMAND yildizbullet_test)
endif()
