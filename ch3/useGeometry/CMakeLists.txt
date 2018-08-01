cmake_minimum_required( VERSION 2.8 )
project( geometry )

# 添加Eigen头文件
include_directories( "/usr/include/eigen3" )

# don't have to use absolute path for adding include file
find_package(PkgConfig)
pkg_check_modules(EIGEN REQUIRED eigen3)
#pkg_search_module(EIGEN REQUIRED eigen3)
include_directories( ${EIGEN_INCLUDE_DIRS} )

add_executable( eigenGeometry eigenGeometry.cpp )
