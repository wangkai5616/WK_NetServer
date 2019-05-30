# WK_NetServer
## 简介 
本项目为C++11编写的基于epoll的多线程网络服务器框架，应用层实现了简单的HTTP服务器HttpServer和一个回显服务器EchoServer，其中HTTP服务器实现了HTTP的解析和Get方法请求，目前支持静态资源访问，支持HTTP长连接；该框架不限于这两类服务器，用户可根据需要编写应用层服务。 

## 并发模型
![Image text](https://raw.githubusercontent.com/wangkai5616/WK_NetServer/master/img-folder/1a5cdf3c6a358e7f471056aafc541aa6_70.png)

## 技术栈
* 使用epoll边沿触发的IO多路复用技术，非阻塞IO，使用Reactor模式  
* 使用多线程充分利用多核CPU，并使用线程池避免线程频繁创建销毁的开销
* 线程池做优化处理，更加高效
* 使用基于时间轮的定时器关闭超时请求
* 线程模型将划分为主线程、IO线程和worker线程，主线程接收客户端连接（accept），并通过Round-Robin策略分发给IO线程，IO线程负责连接管理（即事件监听和读写操作），worker线程负责业务计算任务（即对数据进行处理，应用层处理复杂的时候可以开启）
* 应用层维护一个发送缓冲区和一个接收缓冲区
* 使用eventfd实现了线程的异步唤醒
* 采用智能指针管理多线程下的对象资源
* 使用状态机解析了HTTP请求，支持HTTP长连接
* 支持优雅关闭连接
 
## 代码统计
![Image text](https://github.com/wangkai5616/WK_NetServer/blob/master/img-folder/%E4%BB%A3%E7%A0%81%E7%BB%9F%E8%AE%A1.png)
