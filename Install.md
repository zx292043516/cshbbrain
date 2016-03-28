#Introduction how to install config run and test CshBBrain.

# Introduction #

Introduction how to install config run and test CshBBrain.


# Details #
安装配置运行

1.项目的安装

从http://code.google.com/p/cshbbrain/downloads/list 下载源代码包，解压。从Eclipse 导入项目。 或直接从Eclipse通过svn从http://cshbbrain.googlecode.com/svn/trunk/下载获取项目代 码 。在Eclipse编译项目没有错误提示即成功（项目编译要求jdk1.6及以上版本）。

2.项目的配置

2.1项目系统参数配置

项目参数文件位置：src/com/jason/config.properties
项目系统参数列表：
#the port of the server
#服务器所使用的端口
port=9090

#the priority of the thread in pool
#服务器工作线程的优先级，使用默认优先级即可
maxPriority=5

#the tmp folder
#服务器使用的默认临时文件夹
tmpRoot=e:/tmp/

#the factor of the work process thread per CPU kernel
#业务处理线程CPU内核因子，例如设置为5则表示每个CPU核将创建5个处理线程，如果你的服务器有4个内核，那么将创建5\*4=20个处理线程
requestWorker=5

#the factor of the read writer monitor thread per CPU kernel
#网络数据读写监听线程CPU内核因子，例如设置为1则表示系统将为每个内核创建1个数据读写监听线程，你可以根据自己服务器的性能和需要配置2，4，8个读写监听线程每内核；设置将更加灵活
monitorWorker=1

#the buffer size of the read buffer,unit is KB
#网络数据读取缓存大小，单位是KB
readBuffer=5

#the buffer size of the write buffer,unit is KB
#网络数据发送缓存大小，单位是KB
writeBuffer=64

#the send buffer size of the system sockect
#系统相关的Sockect数据发送缓冲区大小，单位KB
sockectSendBufferSize=64

#the receive buffer of the system socket
#系统相关的Sockect数据接收缓冲区大小，单位KB
sockectReceiveBufferSize=5

#wheather the connection keep alive,1:keep alive,0:not keep alive
#设置服务器处理的连接是长连接，还是端连接，websocket服务器默认为长连接，不可更改
keepConnect=1

#the count of blank read
#设置服务器端空读多少次之后放弃读取客户端的数据
zoreFetchCount = 10

#the min size and the max size of the buffer pool
#设置缓冲区池的最大值和最小值
minBufferPoolSize=1000
maxBufferPoolSize=1000

#whether open the broadcast thread
#设置系统是否开启广播线程
broadSwitch=0


2.2系统日志配置

系统日志文件位置：src/log4j.properties
日志的配置请按照标准的log4j日志进行配置即可

3.项目运行

找到src/com/jason/server/ws/Server.java文件，作为application运行即可启动程序。
服务器启动成功后，默认会输出如下日志：
16:26:35,576  INFO MasterServer:232 - 数据读取回写监听线程创建成功：请求数据传输监听线程0
16:26:35,576  INFO MasterServer:467 - 请求处理调度线程创建完毕
16:26:35,592  INFO MasterServer:232 - 数据读取回写监听线程创建成功：请求数据传输监听线程1
16:26:35,592  INFO MasterServer:467 - 请求处理调度线程创建完毕
16:26:35,592  INFO MasterServer:169 - 消息广播线程创建完毕
16:26:35,592  INFO MasterServer:527 - 连接监听线程创建成功
16:26:35,607  INFO MasterServer:559 - 服务器准备就绪，等待请求到来

4.项目测试

找到项目下的test/chat\_test.html,使用chrome打开，在服务器的后台输出你看到如下信息表示连接建立成功：
16:26:46,248  INFO WebSocketDecoder:111 - the msg received:
GET /echo HTTP/1.1
Upgrade: websocket
Connection: Upgrade
Host: 192.168.1.222:9090
Origin: null
Sec-WebSocket-Key: z1+1r6GtInP+11drO3r7Dg==
Sec-WebSocket-Version: 13
Sec-WebSocket-Extensions: x-webkit-deflate-frame


16:26:46,264  INFO WebSocketDecoder:233 - z1+1r6GtInP+11drO3r7Dg==258EAFA5-E914-47DA-95CA-C5AB0DC85B11
16:26:46,279  INFO WebSocketDecoder:375 - x-webkit-deflate-frame
16:26:46,279  INFO WebSocketDecoder:454 - the response: HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: 0FDvRkfYrdLsbNBFPe+SoM010x0=
Sec-WebSocket-Origin: null
Sec-WebSocket-Location: ws://192.168.1.222:9090/echo

在文本输入框中随便输入一串字符abc,服务器返回

`jason,the msg is : abc`

那么恭喜你已经成功安装配置好项目，你可以试着在项目中添加你自己的业务了。