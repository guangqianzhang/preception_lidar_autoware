cmake_minimum_required(VERSION 2.8.3)
project(visualizer)

find_package(catkin REQUIRED COMPONENTS
  autoware_msgs
  cv_bridge
  geometry_msgs
  image_transport
  roscpp
  sensor_msgs
  tf
  visualization_msgs
)

catkin_package()

find_package(OpenCV 3 REQUIRED)
find_package(Eigen3 QUIET)

if(NOT EIGEN3_FOUND)
  find_package(cmake_modules REQUIRED)
  find_package(Eigen REQUIRED)
  set(EIGEN3_INCLUDE_DIRS ${EIGEN_INCLUDE_DIRS})
  set(EIGEN3_LIBRARIES ${EIGEN_LIBRARIES})
else()
  set(EIGEN3_INCLUDE_DIRS ${EIGEN3_INCLUDE_DIR})
endif()

#Rviz Marker visualization
add_executable(visualize_detected_objects
  include/visualize_detected_objects.h
  src/visualize_detected_objects_main.cpp
  src/visualize_detected_objects.cpp
)

target_include_directories(visualize_detected_objects PRIVATE
  include
  ${OpenCV_INCLUDE_DIR}
  ${catkin_INCLUDE_DIRS}
  ${Boost_INCLUDE_DIRS}
  ${EIGEN3_INCLUDE_DIRS}
)

target_link_libraries(visualize_detected_objects
  ${OpenCV_LIBRARIES}
  ${EIGEN3_LIBRARIES}
  ${catkin_LIBRARIES}
)

add_dependencies(visualize_detected_objects
  ${catkin_EXPORTED_TARGETS}
)

#Image Rect Visualization
add_executable(visualize_rects
  include/visualize_rects.h
  src/visualize_rects_main.cpp
  src/visualize_rects.cpp
)

target_include_directories(visualize_rects PRIVATE
  include
  ${OpenCV_INCLUDE_DIR}
  ${catkin_INCLUDE_DIRS}
)

target_link_libraries(visualize_rects
  ${OpenCV_LIBRARIES}
  ${catkin_LIBRARIES}
)

add_dependencies(visualize_rects
  ${catkin_EXPORTED_TARGETS}
)

install(
  TARGETS
    visualize_detected_objects
    visualize_rects
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
install(DIRECTORY models/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/models
)
