cmake_minimum_required( VERSION 2.8 )
project( visualizeGeometry )

set(CMAKE_CXX_FLAGS "-std=c++11")

# 添加Eigen头文件
include_directories( "/usr/include/eigen3" )

# 添加Pangolin依赖
find_package( Pangolin )
include_directories( ${Pangolin_INCLUDE_DIRS} )
MESSAGE(STATUS "${Pangolin_INCLUDE_DIRS}")

# don't have to use absolute path for adding include file
find_package(PkgConfig)
pkg_check_modules(EIGEN REQUIRED eigen3)
#pkg_search_module(EIGEN REQUIRED eigen3)
include_directories( ${EIGEN_INCLUDE_DIRS} )

add_executable( visualizeGeometry visualizeGeometry.cpp )
target_link_libraries( visualizeGeometry ${Pangolin_LIBRARIES} )
