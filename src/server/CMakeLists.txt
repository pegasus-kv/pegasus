set(MY_PROJ_NAME "pegasus_server")
project(${MY_PROJ_NAME} C CXX)

# Source files under CURRENT project directory will be automatically included.
# You can manually set MY_PROJ_SRC to include source files under other directories.
set(MY_PROJ_SRC "")

# Search mode for source files under CURRENT project directory?
# "GLOB_RECURSE" for recursive search
# "GLOB" for non-recursive search
set(MY_SRC_SEARCH_MODE "GLOB")

set(MY_PROJ_INC_PATH 
    "../include"
    "../base"
    "../../rocksdb/include"
    "${DSN_ROOT}/include/ext")

set(MY_PROJ_LIBS
    dsn_layer2_stateful_type1
    dsn_meta_server
    dsn.replication.clientlib
    dsn.replication.ddlclient
    dsn.failure_detector
    dsn.failure_detector.multimaster
    dsn.replication.zookeeper_provider
    pegasus_client_static
    zookeeper_mt
    event
    )

if (UNIX)
    set(MY_PROJ_LIBS rocksdb ${MY_PROJ_LIBS} z bz2 snappy rt aio pthread)
else()
    set(MY_PROJ_LIBS rocksdblib ${MY_PROJ_LIBS} rpcrt4)
endif()

set(MY_PROJ_LIB_PATH "../../rocksdb" "../ext/libevent/lib")

set(MY_BOOST_PACKAGES system filesystem)

set(MY_BINPLACES "${CMAKE_CURRENT_SOURCE_DIR}/config.ini")

if (UNIX)
    SET(CMAKE_INSTALL_RPATH ".")
    SET(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)
endif()

dsn_add_executable()
