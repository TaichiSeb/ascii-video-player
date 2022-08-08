cmake_minimum_required(VERSION 3.23)

project(AsciiVideoPlayer)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(CMAKE_DEBUG_POSTFIX d)

include(ExternalProject)
ExternalProject_Add(
opencv
GIT_REPOSITORY https://github.com/opencv/opencv.git
GIT_TAG 4.6.0

#PREFIX "${CMAKE_BINARY_DIR}/external/opencv-prefix"
#SOURCE_DIR "${CMAKE_BINARY_DIR}/external/opencv-source"
#BINARY_DIR "${CMAKE_BINARY_DIR}/external/opencv-build"
CMAKE_ARGS -DCMAKE_BUILD_TYPE=Release -DOPENCV_INSTALL_BINARIES_PREFIX= -DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_BINARY_DIR}/external/opencv -DBUILD_TESTS=OFF -DBUILD_PERF_TESTS=OFF
BUILD_COMMAND ${CMAKE_COMMAND} --build . --config Release
LOG_DOWNLOAD ON
LOG_CONFIGURE ON
LOG_BUILD ON
)

include_directories(${CMAKE_BINARY_DIR}/external/opencv/include)
link_directories(${CMAKE_BINARY_DIR}/external/opencv/lib)

add_executable(AsciiVideoPlayer AsciiVideoPlayer.cpp)

target_link_libraries(AsciiVideoPlayer opencv_core460 opencv_videoio460 opencv_imgproc460 opencv_imgcodecs460)

install(TARGETS AsciiVideoPlayer DESTINATION bin)
install(FILES "${CMAKE_BINARY_DIR}/external/opencv/bin/opencv_core460${CMAKE_SHARED_LIBRARY_SUFFIX}" DESTINATION bin)
install(FILES "${CMAKE_BINARY_DIR}/external/opencv/bin/opencv_videoio460${CMAKE_SHARED_LIBRARY_SUFFIX}" DESTINATION bin)
install(FILES "${CMAKE_BINARY_DIR}/external/opencv/bin/opencv_imgproc460${CMAKE_SHARED_LIBRARY_SUFFIX}" DESTINATION bin)
install(FILES "${CMAKE_BINARY_DIR}/external/opencv/bin/opencv_imgcodecs460${CMAKE_SHARED_LIBRARY_SUFFIX}" DESTINATION bin)
