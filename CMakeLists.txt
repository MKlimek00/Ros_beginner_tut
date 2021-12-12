cmake_minimum_required(VERSION 3.0.2)
project(begginer_tutorials)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  message_generation
)

## Generate messages in the 'msg' folder
 add_message_files(
   FILES
   Num.msg
)

## Generate services in the 'srv' folder
 add_service_files(
   FILES
   AddTwoInts.srv
)


## Generate added messages and services with any dependencies listed here
generate_messages(
   DEPENDENCIES
   std_msgs

)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES begginer_tutorials
  CATKIN_DEPENDS roscpp rospy std_msgs message_runtime
  DEPENDS system_lib
)

###########
## Build ##
###########

include_directories(
  include 
  ${catkin_INCLUDE_DIRS}
)

#talker
add_executable(talker_node src/talker.cpp)
target_link_libraries(talker_node ${catkin_LIBRARIES})
add_dependencies(talker_node begginer_tutorials_generate_messages_cpp)

#listener
add_executable(listener_node src/listener.cpp)
target_link_libraries(listener_node ${catkin_LIBRARIES} )
add_dependencies(listener_node begginer_tutorials_generate_messages_cpp)

#service
add_executable(add_two_ints_server src/add_two_ints_server.cpp)
target_link_libraries(add_two_ints_server  ${catkin_LIBRARIES} )
add_dependencies(add_two_ints_server begginer_tutorials_generate_messages_cpp)

#client
add_executable(add_two_ints_client src/add_two_ints_client.cpp)
target_link_libraries(add_two_ints_client  ${catkin_LIBRARIES} )
add_dependencies(add_two_ints_client begginer_tutorials_generate_messages_cpp)








