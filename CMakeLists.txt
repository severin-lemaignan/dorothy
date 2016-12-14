cmake_minimum_required(VERSION 2.8.3)
project(dorothy)

find_package(catkin REQUIRED COMPONENTS 
        naoqi_driver
        gazr 
        ros_markers
        std_msgs
        tf 
        cv_bridge 
        image_transport 
        image_geometry 
        nodelet
        chilitags_catkin)

catkin_package()

include_directories(include ${catkin_INCLUDE_DIRS})

add_definitions(-std=c++11)

set(LIBS 
    ${catkin_LIBRARIES}
    ${OpenCV_LIBRARIES}
    )

add_executable(sandtray_localisation src/chilitagsdetector.cpp src/sandtray_localisation.cpp)
target_link_libraries(sandtray_localisation ${LIBS})

install(TARGETS sandtray_localisation 
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(FILES
    launch/dorothy.launch
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
)

install(FILES
    config/chilitags_config.yml
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/config
)

