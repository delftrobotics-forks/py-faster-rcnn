cmake_minimum_required(VERSION 3.1)
project(FasterRCNN)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/modules/")

find_package(Caffe REQUIRED)
find_package(CUDA REQUIRED)
find_package(YamlCpp REQUIRED)

include_directories(
	${Caffe_INCLUDE_DIRS}
	${CUDA_INCLUDE_DIRS}
	${YamlCpp_INCLUDE_DIRS}
)

cuda_add_library(fasterrcnn MODULE
	src/roi_pooling_layer.cpp
	src/roi_pooling_layer.cu
	src/smooth_L1_loss_layer.cpp
	src/smooth_L1_loss_layer.cu
)
target_link_libraries(fasterrcnn
	${Caffe_LIBRARIES}
	${CUDA_LIBRARIES}
	${YamlCpp_LIBRARIES}
)
