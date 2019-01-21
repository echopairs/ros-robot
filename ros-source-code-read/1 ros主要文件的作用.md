```
io.h 								对epoll的操作接口
poll_set.h/cpp  					对epoll的封装，对socket添加读写到epoll的处理
poll_manager.h/cpp					管理poll_set

transport.h/cpp 					传输层抽象类,对socket的封装，设置及调用读/写/丢失链接的回调
transport_tcp.h/cpp 				TCP实现transport抽象类，提供对socket的原始操作接口(读写监听建立链接等)
transport_udp.h/cpp					UDP实现transport抽象类

connection.h/cpp 					对Transport层的封装，用于读写固定长度的数据，及调用一系列的读写结束后的回调
connection_manager.h/cpp 			管理节点的所有的链接，包括启动节点监听/处理有新的链接请求生成connection/关闭删除connection/处理新链接上来的数据等

service_server_Link.h/cpp			rpc cleint端调用生成，通过connection层发送请求和接收服务端反馈的响应
service_client_link.h/cpp   		rpc server端由connection_manager生成，用于处理client端发送过来的rpc请求并响应

service_client.h/cpp 				Provides a handle-based interface to service client connections
service_manager.h/cpp 				创建rpc client端 的请求对象，创建rpc server端响应对象
service_publication.h/cpp 			rpc request读取后由service_client_link传入service_publication处理

callback_queue_interface.h  		回调队列列表接口
callback_queue.h/cpp 				默认的回调队列，处理接收到的回调

intraprocess_subscriber_link.h/cpp  pub端节点处理内部sub
transport_subscriber_link.h/cpp		pub端接收到sub请求时建立链接，后用来发送消息到sub端

intraprocess_publisher_link.h/cpp 	sub端节点处理内部pub
transport_publisher_link.h/cpp  	sub端check topic后获取都pub端的地址，connetct到pub后发送头部

publication.h/cpp 					pub端用来处理发送消息
subscription.h/cpp					sub端用于连接pub端，接收消息，处理消息
subscription_queue.h/cpp 			sub端 处理subscription
transport_hints.h/cpp 				设置连接类型

init.h/init.cpp 					初始化节点
node_handle.h/cpp 					节点操作列表,用于创建sub/pub/server/client
advertise_options.h/cpp 			设置pub属性

publisher.h/cpp						pub操作的文件
subscriber.h/cpp					sub操作的文件
service_client.h/cpp				client操作的文件
service_server.h/cpp 				server操作的文件

spinner.h/cpp						循环从任务队列中获取任务执行
publisher_link.h/cpp				sub端接收处理pub端发送过来消息的接口(TransportPublisherLink)
```