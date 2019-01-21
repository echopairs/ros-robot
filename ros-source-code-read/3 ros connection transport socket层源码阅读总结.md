## 本文主要内容

本文是对从socket到链接层源码阅读文档的总结

[3.1 ros底层对socket和事件的管理和封装](http://note.youdao.com/noteshare?id=40edcaccdb75920504018e806a4bf669&sub=7394E7C61D594A6EB634490429B5A741)

[3.2 ros Transport层源码阅读](http://note.youdao.com/noteshare?id=07e5e319605be7f4bb58ec92fd72b083&sub=F8FD6A3C34364E1880E41C06A2C01BCD)

[3.3 ros connection层源码阅读](http://note.youdao.com/noteshare?id=1659dfe00bb69efcbaa62be6294d1e05&sub=3FCF8336B263435C86042BA1F7598458)

**该层的作用:**
1. 封装系统网络操作的api屏蔽不同的通信协议(UDP/TCP)
2. 对上层提供读写操作的接口

**网络线程模型:**
```
epoll ET模型实现Reactor模式，单线程非阻塞进行IO读写，回调构建任务后(rpc请求/pub数据)压入到节点任务队列后进行下一个fd的读写。
```


## 架构层次图

![部分流程图](https://github.com/echopairs/blog/blob/master/pic/jz/part.png?raw=true)

**如上图所示，通过封装socket、transport层抽象出Connect接口提供给上层进行读写的调用**

**PollManager/PollSet层**

1. 封装对socket、网络事件、件定时操作、epoll的操作，向transport层提供相应的接口
2. 事件触发后调用tranport注册的各种事件回调函数(周期性、网络事件)

**transport层**

1. 屏蔽端对端链接方式的差异，向上层提供读写接口及设置相关的回调函数

**Connect层**

1. 封装Transport层，提供读写数据及数据头部的接口(==通过异步回调的方式==)
2. 为上层(pub/sub/server/client)提供基于包传递的网络传输的接口(面向报文)
