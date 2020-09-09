find_package(Protobuf REQUIRED)
find_package(std_msgs REQUIRED)

set(PROTOBUF_IMPORT_DIRS)
foreach(ITR ${GAZEBO_INCLUDE_DIRS})
  if(ITR MATCHES ".*gazebo-[0-9.]+$")
    set(PROTOBUF_IMPORT_DIRS "${ITR}/gazebo/msgs/proto")
  endif()
endforeach()

set (msgs
	Float.proto
)
PROTOBUF_GENERATE_CPP(PROTO_SRCS PROTO_HDRS ${msgs})
add_library(my_msgs SHARED ${PROTO_SRCS})
target_link_libraries(my_msgs ${PROTOBUF_LIBRARY})
