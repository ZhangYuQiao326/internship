workflow认为**一切资源都是可以异步调度的**，支持的资源对接如下：

![image-20240514093105245](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405140931430.png)

![image-20240514102701203](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405141027393.png)

**Workflow**的src/kernel目录里，包含了以下独立的模块，基本都是C和简单C++语法实现的，没有复杂的语法，每一个模块都很小，都可以单独拿出来学习：

- **poller**，可以学习如何使用epoll
- **thrdpool**，经典线程池实现
- **msgqueue**，消息队列实现
- **Communicator**，[异步网络通信器](https://www.zhihu.com/search?q=异步网络通信器&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A3151447745})，包括了基本的目标管理和[负载均衡](https://www.zhihu.com/search?q=负载均衡&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A3151447745})
- **Executor**，包含计算调度算法的执行器
- **IO_Service**，异步文件IO

![image-20240514114039902](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures/img/202405141140982.png)