# 最低 CMake 版本要求
cmake_minimum_required(VERSION 3.10)

# 项目信息
project(ChatRoomProject)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 17)

# 添加头文件目录，将 websocketpp 和 MySQL 的头文件路径加入到项目中
include_directories(include include/websocketpp ${MySQL_INCLUDE_DIRS})

# 设置 MySQL 头文件和库路径 (请替换为实际的 MySQL 安装路径)
set(MySQL_INCLUDE_DIRS "C:/Program Files/MySQL/MySQL Server 5.6/include")
set(MySQL_LIBRARIES "C:/Program Files/MySQL/MySQL Server 5.6/lib/libmysql.lib")

# 设置源文件列表
set(SERVER_SRC
    src/main.cpp
    src/server.cpp
    src/websocket.hpp
    src/database.cpp
)

set(CLIENT_SRC
    src/client.cpp
    src/websocket.hpp
    src/database.cpp
)

# 添加 WebSocket++ 库
# 确保 websocketpp 目录中包含头文件即可，不需要额外链接库

# 创建 server 和 client 可执行文件
add_executable(server ${SERVER_SRC})
add_executable(client ${CLIENT_SRC})

# 链接 MySQL 库
target_link_libraries(server ${MySQL_LIBRARIES} pthread)
target_link_libraries(client ${MySQL_LIBRARIES} pthread)



