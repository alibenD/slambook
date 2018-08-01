cmake_minimum_required( VERSION 2.8 )
project( useSophus )

IF("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
   SET(CMAKE_CXX_FLAGS_DEBUG  "-O0 -g")
   SET(CMAKE_CXX_FLAGS_RELEASE "-O3")
   SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror -Wextra -Wno-deprecated-register -Wno-deprecated-register -Qunused-arguments -fcolor-diagnostics")
ELSEIF("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
   SET(CMAKE_CXX_FLAGS_DEBUG  "-O0 -g")
   SET(CMAKE_CXX_FLAGS_RELEASE "-O3")
   SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror -Wextra -std=c++11 -Wno-deprecated-declarations -ftemplate-backtrace-limit=0")
   SET(CMAKE_CXX_FLAGS_COVERAGE "${CMAKE_CXX_FLAGS_DEBUG} --coverage -fno-inline -fno-inline-small-functions -fno-default-inline")
   SET(CMAKE_EXE_LINKER_FLAGS_COVERAGE "${CMAKE_EXE_LINKER_FLAGS_DEBUG} --coverage")
   SET(CMAKE_SHARED_LINKER_FLAGS_COVERAGE "${CMAKE_SHARED_LINKER_FLAGS_DEBUG} --coverage")
ELSEIF(CMAKE_CXX_COMPILER_ID MATCHES "^MSVC$")
   ADD_DEFINITIONS("-D _USE_MATH_DEFINES /bigobj /wd4305 /wd4244 /MP")
ENDIF()

# 为使用 sophus，您需要使用find_package命令找到它
find_package( Sophus REQUIRED )
include_directories( ${Sophus_INCLUDE_DIRS} )


find_package(PkgConfig)
pkg_check_modules(EIGEN REQUIRED eigen3)
#pkg_search_module(EIGEN REQUIRED eigen3)
include_directories( ${EIGEN_INCLUDE_DIRS} )
MESSAGE(STATUS "${EIGEN_INCLUDE_DIRS}")

add_executable( useSophus useSophus.cpp )
target_link_libraries( useSophus ${Sophus_LIBRARIES} )
