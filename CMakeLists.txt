cmake_minimum_required(VERSION 3.5)
project(ExternalProjectDemo)

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake/" ${CMAKE_MODULE_PATH})

# Boost
find_package(Boost REQUIRED COMPONENTS iostreams system filesystem)
message(STATUS "Boost libs: " ${Boost_LIBRARIES})
if(Boost_FOUND)
    include_directories(${Boost_INCLUDE_DIRS})
    include_directories(${Boost_INCLUDE_DIR})
    link_directories(${Boost_LIBRARY_DIRS})
endif()


# OpenCV
find_package(OpenCV COMPONENTS core imgproc objdetect highgui REQUIRED)
if(OpenCV_FOUND)
    include_directories(${OpenCV_INCLUDE_DIR})
endif()
message(STATUS "OpenCV v.: " ${OpenCV_VERSION})
message(STATUS "OpenCV libs: " ${OpenCV_LIBS})

# OpenTBB
find_package(TBB REQUIRED)
if(TBB_FOUND)
    include_directories(TBB_INCLUDE_DIRS)
endif()
message(STATUS "OpenTBB libs: " ${TBB_LIBRARIES})

# dlib
find_package(dlib REQUIRED)
message(STATUS "dlib v.: " ${dlib_VERSION})
message(STATUS "dlib libs: " ${dlib_LIBS})

# 3rd part libraries
include(3rdlibrary/CMakeLists.txt)
# Beast lib
message(STATUS "Beast includes: " ${BEAST_INCLUDE_DIR})
include_directories(${BEAST_INCLUDE_DIR})
# OpenFace lib
message(STATUS "OpenFace includes: " ${OPENFACE_INCLUDE_DIR})
message(STATUS "OpenFace libs: " ${OPENFACE_LIBRARY_DIR})
include_directories(${OPENFACE_INCLUDE_DIR})
link_directories(${OPENFACE_LIBRARY_DIR})

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(SOURCE_FILES main.cpp)
add_executable(ExternalProjectDemo ${SOURCE_FILES})

add_dependencies(ExternalProjectDemo Beast OpenFace)

target_link_libraries(ExternalProjectDemo LandmarkDetector)
target_link_libraries(ExternalProjectDemo dlib)
target_link_libraries(ExternalProjectDemo ${OpenCV_LIBS} ${Boost_LIBRARIES} ${TBB_LIBRARIES} -lpthread )