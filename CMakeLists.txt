cmake_minimum_required(VERSION 2.8.3)
project(GMM)

find_package(catkin REQUIRED COMPONENTS
  cv_bridge
  image_transport
  roscpp
  sensor_msgs
  std_msgs
  actionlib
  actionlib_msgs
  genmsg
)

find_package(OpenCV REQUIRED)

find_package(catkin REQUIRED genmsg actionlib_msgs actionlib)

add_action_files(DIRECTORY action FILES mission.action)

generate_messages(DEPENDENCIES actionlib_msgs)

catkin_package(
  CATKIN_DEPENDS cv_bridge image_transport roscpp std_msgs sensor_msgs
)

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
)

add_executable(kalman src/Kalman.cpp)
target_link_libraries(kalman ${OpenCV_LIBRARIES}  ${catkin_LIBRARIES})

add_executable(gmm src/gmm.cpp)
target_link_libraries(gmm  ${OpenCV_LIBRARIES}  ${catkin_LIBRARIES})

add_executable(pub src/publisher.cpp)
target_link_libraries(pub  ${OpenCV_LIBRARIES}  ${catkin_LIBRARIES})

add_executable(sub src/subscriber.cpp)
target_link_libraries(sub  ${OpenCV_LIBRARIES}  ${catkin_LIBRARIES})
