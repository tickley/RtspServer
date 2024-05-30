cmake_minimum_required(VERSION 3.4.1)
project(rtsp_project)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS "-pthread")

# 设置编译选项
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2")

# mpp
set(MPP_PATH ${CMAKE_CURRENT_SOURCE_DIR}/include/mpp)
set(MPP_LIBS ${MPP_PATH}/${CMAKE_SYSTEM_NAME}/librockchip_mpp.so)
include_directories(${MPP_PATH}/include)

# 添加头文件搜索路径
include_directories(src)

# 添加源文件
file(GLOB NET_SOURCES src/net/*.cpp)
file(GLOB XOP_SOURCES src/xop/*.cpp)
file(GLOB RTSP_CAM_SERVER_SOURCE example/rtsp_camera.cpp)
file(GLOB RTSP_SERVER_SOURCE example/rtsp_server.cpp)
file(GLOB RTSP_PUSHER_SOURCE example/rtsp_pusher.cpp)
file(GLOB RTSP_H264_FILE_SOURCE example/rtsp_h264_file.cpp)



# 生成目标可执行文件
add_executable(rtsp_camera 
    src/camera/mpi_encoder.c
    src/camera/camera_source.c
    ${NET_SOURCES} 
    ${XOP_SOURCES} 
    ${RTSP_CAM_SERVER_SOURCE}
)

add_executable(rtsp_server ${NET_SOURCES} ${XOP_SOURCES} ${RTSP_SERVER_SOURCE})
add_executable(rtsp_pusher ${NET_SOURCES} ${XOP_SOURCES} ${RTSP_PUSHER_SOURCE})
add_executable(rtsp_h264_file ${NET_SOURCES} ${XOP_SOURCES} ${RTSP_H264_FILE_SOURCE})

target_link_libraries(rtsp_camera 
  ${MPP_LIBS}
)

# install target and libraries
set(CMAKE_INSTALL_PREFIX ${CMAKE_SOURCE_DIR}/install)
install(TARGETS rtsp_camera DESTINATION ./)
install(TARGETS rtsp_server DESTINATION ./)
install(TARGETS rtsp_pusher DESTINATION ./)
install(TARGETS rtsp_h264_file DESTINATION ./)
install(PROGRAMS ${MPP_LIBS} DESTINATION lib)