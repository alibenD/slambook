cmake_minimum_required( VERSION 2.8 )
project( useEigen )

set( CMAKE_BUILD_TYPE "Release" )
set( CMAKE_CXX_FLAGS "-O3" )

# 添加Eigen头文件
#include_directories( "/usr/include/eigen3" )

# For finding Eigen by pkg-config,
# don't have to use absolute path for adding include file
find_package(PkgConfig)
pkg_check_modules(EIGEN REQUIRED eigen3)
#pkg_search_module(EIGEN REQUIRED eigen3)
include_directories( ${EIGEN_INCLUDE_DIRS} )
MESSAGE(STATUS "${EIGEN_INCLUDE_DIRS}")

# in osx and brew install
# include_directories( /usr/local/Cellar/eigen/3.3.3/include/eigen3 )

add_executable( eigenMatrix eigenMatrix.cpp )
