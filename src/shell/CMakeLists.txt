set(MY_PROJ_NAME "pegasus_shell")
project(${MY_PROJ_NAME} C CXX)

# Source files under CURRENT project directory will be automatically included.
# You can manually set MY_PROJ_SRC to include source files under other directories.
set(MY_PROJ_SRC "linenoise/linenoise.c" "sds/sds.c")

# Search mode for source files under CURRENT project directory?
# "GLOB_RECURSE" for recursive search
# "GLOB" for non-recursive search
set(MY_SRC_SEARCH_MODE "GLOB")

set(MY_PROJ_INC_PATH "../include" "../base")

set(MY_PROJ_LIBS
    dsn.replication.tool
    dsn_replica_server
    dsn_replication_common
    dsn.replication.ddlclient
    dsn.block_service.local
    dsn.block_service.fds
    dsn.failure_detector
    dsn.failure_detector.multimaster
    pegasus_client_static
    galaxy-fds-sdk-cpp
    PocoNet
    PocoFoundation
    PocoNetSSL
    PocoJSON
    crypto
    fmt
    pegasus_geo_lib
    s2
    )

if (UNIX)
    set(MY_PROJ_LIBS rocksdb ${MY_PROJ_LIBS} z bz2 snappy rt aio pthread)
else()
    set(MY_PROJ_LIBS rocksdblib ${MY_PROJ_LIBS} rpcrt4)
endif()

set(MY_PROJ_LIB_PATH "../../rocksdb/build")

set(MY_BINPLACES "${CMAKE_CURRENT_SOURCE_DIR}/config.ini")

set(MY_BOOST_PACKAGES system filesystem)

if (UNIX)
    SET(CMAKE_INSTALL_RPATH ".")
    SET(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)
endif()

add_definitions(-Wno-attributes)

dsn_add_executable()
dsn_install_executable()
