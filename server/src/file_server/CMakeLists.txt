cmake_minimum_required(VERSION 3.12)
PROJECT(fileserver)

AUX_SOURCE_DIRECTORY(./ SRC_LIST)

#SET(LIBRARY_OUTPUT_PATH ./)
SET(EXECUTABLE_OUTPUT_PATH  ${CMAKE_SOURCE_DIR}/run/bin)

SET(UUID_NAME uuid)


#设置自己mac os的openssl的路径
if(APPLE)
    SET(UUID_NAME )
endif()


ADD_DEFINITIONS( -g -W -Wall -D_REENTRANT -D_FILE_OFFSET_BITS=64 -DAC_HAS_INFO
-DAC_HAS_WARNING -DAC_HAS_ERROR -DAC_HAS_CRITICAL -DTIXML_USE_STL
-DAC_HAS_DEBUG -DLINUX_DAEMON -std=c++11)


ADD_EXECUTABLE(file_server ${SRC_LIST} )

TARGET_LINK_LIBRARIES(file_server base )
 
target_include_directories(file_server PRIVATE
        .
        ../pkg/include
        ../pb/protocol
       /usr/local/include
        )

target_link_directories(
        file_server PRIVATE
        .
        ../pkg/lib
        /usr/local/lib
)