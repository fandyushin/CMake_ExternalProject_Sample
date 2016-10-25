include(ExternalProject)

set(BEAST_ROOT ${CMAKE_BINARY_DIR}/3rdlibrary/Beast)

ExternalProject_Add(Beast
        PREFIX ${BEAST_ROOT}
        GIT_REPOSITORY "https://github.com/vinniefalco/Beast.git"
        GIT_TAG "325f579"
        CONFIGURE_COMMAND ""
        BUILD_COMMAND ""
        INSTALL_COMMAND ""
        )

ExternalProject_Get_Property(Beast SOURCE_DIR)
set(BEAST_INCLUDE_DIR ${SOURCE_DIR}/include)

set(OPENFACE_TAR "/home/fandyushin/Downloads/OpenFace-master.zip")
set(OPENFACE_ROOT ${CMAKE_BINARY_DIR}/3rdlibrary/OpenFace)

ExternalProject_Add(OpenFace
        PREFIX ${OPENFACE_ROOT}
        URL ${OPENFACE_TAR}
        CMAKE_ARGS -DCMAKE_BUILD_TYPE=RELEASE
        BUILD_COMMAND make LandmarkDetector -j
        INSTALL_COMMAND ""
        )

ExternalProject_Get_Property(OpenFace SOURCE_DIR)
ExternalProject_Get_Property(OpenFace BINARY_DIR)

set(OPENFACE_INCLUDE_DIR ${SOURCE_DIR}/lib/local/LandmarkDetector/include)
set(OPENFACE_LIBRARY_DIR ${BINARY_DIR}/lib/local/LandmarkDetector)