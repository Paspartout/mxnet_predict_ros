cmake_minimum_required(VERSION 2.8.3)
project(mxnet_predict)

## Compile options needed to compile mxnet standalone
add_compile_options(-DMSHADOW_USE_CUDA=0 -DMSHADOW_USE_MKL=0 -DMSHADOW_RABIT_PS=0 -DMSHADOW_DIST_PS=0 -DDMLC_LOG_STACK_TRACE=0)
add_compile_options(-DMSHADOW_FORCE_STREAM -DMXNET_USE_OPENCV=0 -DMXNET_PREDICT_ONLY=1)
add_compile_options(-std=c++11 -Wno-unknown-pragmas -Wall)

find_package(catkin REQUIRED)

## BLAS is the only dependence for the minimal mxnet prediction api
find_package(BLAS REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES mxnet_predict
#  CATKIN_DEPENDS other_catkin_pkg
#  DEPENDS system_lib
)

include_directories(
  include
  # blas_include dirs?
)

add_library(${PROJECT_NAME}
  src/mxnet_predict-all.cc
)

target_link_libraries(${PROJECT_NAME}
  ${catkin_LIBRARIES}
  ${BLAS_LIBRARIES}
)

