cmake_minimum_required(VERSION 3.12)
PROJECT(loginserver)


AUX_SOURCE_DIRECTORY(./ SRC_LIST)

 SET(EXECUTABLE_OUTPUT_PATH  ${CMAKE_SOURCE_DIR}/run/bin)




ADD_DEFINITIONS( -g -W -Wall -D_REENTRANT -D_FILE_OFFSET_BITS=64 -DAC_HAS_INFO
-DAC_HAS_WARNING -DAC_HAS_ERROR -DAC_HAS_CRITICAL -DTIXML_USE_STL
-DAC_HAS_DEBUG -DLINUX_DAEMON -std=c++11)

#INCLUDE_DIRECTORIES(./ ../base ../pb/protocol ../pkg/jsoncpp/ ${PB_INCLUDE_DIR} ${OPENSSL_INCLUDE_DIR})
#LINK_DIRECTORIES(${SRC_DIR}/lib ${Slog_LIB_DIR} ${PB_LIB_DIR} ${OPENSSL_LIB_DIR})

#ADD_XXXX必须在TARGET_LINK_LIBRARIES前面，否则会报错
#ADD_LIBRARY(${PROJECTNAME} SHARED/STATIC ${SRC_LIST})
ADD_EXECUTABLE(login_server ${SRC_LIST})

TARGET_LINK_LIBRARIES(login_server base protobuf-lite pthread ssl crypto)

target_include_directories(
        login_server PRIVATE
        .
        ../pkg/include
        ../pb/protocol
        /usr/local/include
)

target_link_directories(
        login_server PRIVATE
        .
        /usr/local/lib
        ../pkg/lib
)