cmake_minimum_required(VERSION 2.8.3)
project(aslam_serialization)

find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)

#find_package(Protobuf REQUIRED)
#message(WARNING "Protobuf found: ${Protobuf_FOUND}")
#message(WARNING "Protobuf version: ${Protobuf_VERSION}")
#message(WARNING "Protobuf include: ${Protobuf_INCLUDE_DIRS}")
#message(WARNING "Protobuf compiler: ${Protobuf_PROTOC_EXECUTABLE}")

#message(WARNING "wsklgjfldikjglkdfjg ${Protobuf_IMPORT_DIRS} ")
#set(Protobuf_IMPORT_DIRS "${CMAKE_CURRENT_SOURCE_DIR}/proto")
############
# PROTOBUF #
############
#message(WARNING " the freaking headers for proto ${PROTO_HDRS}")

SET(PROTO_DEFNS proto/aslam-serialization/camera.proto
                proto/aslam-serialization/visual-frame.proto)
PROTOBUF_CATKIN_GENERATE_CPP2("proto" PROTO_SRCS PROTO_HDRS ${PROTO_DEFNS})

#############
# LIBRARIES #
#############
cs_add_library(${PROJECT_NAME} ${PROTO_SRCS} ${PROTO_HDRS}
  src/camera-serialization.cc
  src/visual-frame-serialization.cc
)

##########
# GTESTS #
##########
catkin_add_gtest(test_camera_serialization test/test-camera-serialization.cc)
target_link_libraries(test_camera_serialization ${PROJECT_NAME})

catkin_add_gtest(test_visual_frame_serialization test/test-visual-frame-serialization.cc)
target_link_libraries(test_visual_frame_serialization ${PROJECT_NAME})

##########
# EXPORT #
##########
cs_install()
cs_export()
