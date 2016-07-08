##PHP socket 学习
###1. socket_create函数

用于创建socket套接字，
	
参数：`resource socket_create ( int $domain , int $type , int $protocol )`

* `$domain`是domain 参数指定哪个协议用在当前套接字上。（在ipv4 使用AF_INET， 在ipv6使用AF_INET6）
* `$type`  是套接字的类型，主要分为
	1. SOCK\_STREAM 流式套接字 流套接字用于提供面向连接、可靠的数据传输服务。该服务将保证数据能够实现无差错、无重复发送，并按顺序接收 主要用在TCP协议中
	2. SOCK\_DGRAM 数据包套接字 数据包套接字提供了一种无连接的服务。该服务并不能保证数据传输的可靠性，数据有可能在传输过程中丢失或出现数据重复，且无法保证顺序地接收到数据。主要用在UDP协议中
	3. SOCK\_SEQPACKET  提供一个顺序化的、可靠的、全双工的、面向连接的、固定最大长度的数据通信；数据端通过接收每一个数据段来读取整个数据包。
	4. SOCK\_RAW 提供读取原始的网络协议。这种特殊的套接字可用于手工构建任意类型的协议。一般使用这个套接字来实现 ICMP 请求（例如 ping）
* `$protocol` 使用何种协议 SQL_TCP,SQL_UDP
	
###2. socket_bind函数
给套接字绑定名字

参数：`bool socket_bind ( resource $socket , string $address [, int $port = 0 ] )`

* `$socket` 是socket_create创建的套接字
* `$address` 是绑定IP，如果是 AF_INET 族，那么 address 必须是一个四点分法的 IP 地址（例如 127.0.0.1 ），是 AF_UNIX 族，那么 address 是 Unix 套接字一部分（例如 /tmp/my.sock ）
* `$port` 是绑定端口

###3. socket_listen函数
listen函数使用主动连接套接口变为被连接套接口，使得一个进程可以接受其它进程的请求，从而成为一个服务器进程。在TCP服务器编程中listen函数把进程变为一个服务器，并指定相应的套接字变为被动

参数：`bool socket_listen ( resource $socket [, int $backlog = 0 ] )`

* `$socket` socket handel
* `$backlog` 这个参数涉及到一些网络的细节。在进程正理一个一个连接请求的时候，可能还存在其它的连接请求。因为TCP连接是一个过程，所以可能存在一种半连接的状态，有时由于同时尝试连接的用户过多，使得服务器进程无法快速地完成连接请求。如果这个情况出现了，服务器进程希望内核如何处理呢？内核会在自己的进程空间里维护一个队列以跟踪这些完成的连接但服务器进程还没有接手处理或正在进行的连接，这样的一个队列内核不可能让其任意大，所以必须有一个大小的上限。这个backlog告诉内核使用这个数值作为上限。
毫无疑问，服务器进程不能随便指定一个数值，内核有一个许可的范围。这个范围是实现相关的。很难有某种统一，一般这个值会小30以内。

###4. socket_accept函数
将当前PHP进程进入阻塞模式，等待客户端的连接

参数 `resource socket_accept ( resource $socket )`

* `$socket` 是有socket_create创建的一个socket套接字

返回连接成功的资源，利用这个资源可以读取客户端发送的内容（socket_read）,也可以像客户端发送内容(socket_write)

###5. socket_write函数
向一个socket中写入内容

参数 `int socket_write ( resource $socket , string $buffer [, int $length ] )`

* `$socket` socket handel
* `$buffer` 写入的内容
* `$length` 写入的长度

###6. socket_read()函数
读取socket中的内容

参数 `string socket_read ( resource $socket , int $length [, int $type = PHP_BINARY_READ ] )`

* `$socket` 读取的内容
* `$length` 读取的长度
* `$type`   读取内容的的方式，主要是结束的方式

###7. socket_recv()函数
读取socket中的内容

参数 `int socket_recv ( resource $socket , string &$buf , int $len , int $flags )`

* `$socket` 读取的内容
* `$buff` 读取的内容存放的变量
* `$len` 读取内容的最大长度
* `$flags` 接受的方式

###8. socket_connect() 函数
作为客户端连接一个socket

参数 `bool socket_connect ( resource $socket , string $address [, int $port = 0 ] )`

* `$socket` socket handel
* `$address` AF_INET 填写ip地址，AP_UNIX 填写文件地址

###9. socket_last_error()函数
返回上次错误的编号

###10. socket_strerror() 函数
获取上次错误的文字描述

###11. stream_socket_server() 函数
创建一个socket，类似于socket_create() + socket_bind() + socket_listen() 的集合动作

###12. socket_close() 函数
关闭socket


##server的socket编写

1. 创建socket，
2. socket_create() + socket_bind() + socket_listen() 创建出一个socket（其实就是创建个socket的数据结构）
3. 然后利用socket_accept()阻塞进程，监听端口，等待客户端连接
4. 连接成功后，利用socket_read 读取客户端发送的内容，利用socket_write 想客户端发送内容
5. 关闭socket

##Client的socket编写

1. 连接socket，用socket_connet()或者stream_socket_client()或者fsocketopen()
2. 利用socket_read() 和socket_write() 读写内容    fsocketopen() 利用fwrite() 和fread() 读写内容
3. socket_close关闭   fsocket_close() 关闭
