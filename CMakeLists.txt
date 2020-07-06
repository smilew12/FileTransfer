cmake_minimum_required(VERSION 2.6)

project (FILESERVER)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x -g -Wall -O0 -Wno-unused-variable -pthread")

#link_directories(
#    ${PROJECT_SOURCE_DIR}/lib
#	/usr/lib64/mysql/
#)
#
# �Ƽ�ʹ�� CentOS 7.0 ������ϵͳ..dwdwdw
# CentOS 7.0 ������ϵͳĬ�ϰ�װ����mariadb����װ����
# yum install mariadb-server mariadb mariadb-devel
# CentOS 7.0 ����ϵͳĬ�ϰ�װmysql����װ������
# yum install mysql-server mysql mysql-devel

#find_library(MYSQL_LIB libmysqlclient.so /usr/lib64/mysql/)
##���������ݿ���mariadb���㻹��Ҫ��װmariadb-devel�⣻���������ݿ���mysql������Ҫ��װmysql-devel�������������´�����ʾ��
#IF (NOT MYSQL_LIB)
#    MESSAGE(FATAL_ERROR "mysqlclient not found. If your mysql is mariadb, please install mariadb-devel otherwise install mysql-devel.")
#ENDIF(NOT MYSQL_LIB)

set(net_srcs 
base/AsyncLog.cpp
base/SystemConfig
base/Platform.cpp
base/Timestamp.cpp

net/Acceptor.cpp
net/Buffer.cpp
net/Channel.cpp
net/Connector.cpp
net/EpollPoller.cpp
net/EventLoop.cpp
net/EventLoopThread.cpp
net/EventLoopThreadPool.cpp
net/InetAddress.cpp
net/Poller.cpp
net/PollPoller.cpp
net/ProtocolStream.cpp
net/SelectPoller.cpp
net/Sockets.cpp
net/TcpClient.cpp
net/TcpConnection.cpp
net/TcpServer.cpp
net/Timer.cpp
net/TimerQueue.cpp
)

#set(mysqlapi_srcs
#mysqlapi/DatabaseMysql.cpp
#mysqlapi/Field.cpp
#mysqlapi/QueryResult.cpp
#)
#
#set(mysqlmgr_srcs
#mysqlmgr/MysqlManager.cpp
#mysqlmgr/MysqlThrd.cpp
#mysqlmgr/MysqlThrdMgr.cpp
#mysqlmgr/TaskList.cpp
#)
#
set(json_srcs
jsoncpp1.9.0/json_reader.cpp
jsoncpp1.9.0/json_value.cpp
jsoncpp1.9.0/json_writer.cpp
)

set(zlib_srcs
zlib1.2.11/zutil.c
zlib1.2.11/uncompr.c
zlib1.2.11/trees.c
zlib1.2.11/inftrees.c
zlib1.2.11/inflate.c
zlib1.2.11/inffast.c
zlib1.2.11/infback.c
zlib1.2.11/gzwrite.c
zlib1.2.11/gzread.c
zlib1.2.11/gzlib.c
zlib1.2.11/gzclose.c
zlib1.2.11/deflate.c
zlib1.2.11/crc32.c
zlib1.2.11/compress.c
zlib1.2.11/adler32.c
zlib1.2.11/ZlibUtil.cpp
)

set(utils_srcs
utils/StringUtil.cpp
utils/URLEncodeUtil.cpp
utils/MD5.cpp
utils/DaemonRun.cpp
utils/MD5.cpp
)

#set(chatserver_srcs
#chatserversrc/main.cpp
#chatserversrc/ChatServer.cpp
#chatserversrc/ChatSession.cpp
#chatserversrc/UserManager.cpp
#chatserversrc/MsgCacheManager.cpp
#chatserversrc/TcpSession.cpp
#chatserversrc/MonitorSession.cpp
#chatserversrc/MonitorServer.cpp
#chatserversrc/HttpSession.cpp
#chatserversrc/HttpServer.cpp
#chatserversrc/BussinessLogic.cpp)

set(fileserver_srcs
fileserversrc/main.cpp
fileserversrc/FileServer.cpp
fileserversrc/FileSession.cpp
fileserversrc/FileManager.cpp
fileserversrc/TcpSession.cpp)

set(imgserver_srcs
imgserversrc/main.cpp
fileserversrc/FileServer.cpp
fileserversrc/FileSession.cpp
fileserversrc/FileManager.cpp
fileserversrc/TcpSession.cpp)


#add_executable(chatserver ${net_srcs} ${json_srcs}  ${chatserver_srcs} ${mysqlapi_srcs} ${mysqlmgr_srcs} ${zlib_srcs} ${utils_srcs})
#�������Ŀ¼��û�õģ�������ʹ��TARGET_LINK_LIBRARIES���Ӹÿ�
#TARGET_LINK_LIBRARIES(chatserver mysqlclient)

add_executable(fileserver ${net_srcs}  ${fileserver_srcs} ${utils_srcs})
TARGET_LINK_LIBRARIES(fileserver)

add_executable(imgserver ${net_srcs}  ${imgserver_srcs} ${utils_srcs})
TARGET_LINK_LIBRARIES(imgserver)
