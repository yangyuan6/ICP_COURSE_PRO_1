本代码库，没有考虑任何权限、Owner相关的设定，仅为了完成actor创建多个actor class

定义一个LenthyLogger.mo，是一个actor class，由它引用ic-logger/Logger。

主合约是由MyLogger定义，它里面定义了一个loggers，保存LenthyLogger的数组，空间不够则继续创建新的LenthyLogger。

这三者的关系如下：

MyLogger(1) -> LenthyLogger(n).  
LenthyLogger(1) -> ic-logger/Logger(1).  

LenthyLogger: actor class.  
MyLogger: actor.  

MyLogger对外暴露四个四个函数。

print_info为调试使用，在后台打印所有的log。

append为往合约中添加新的log数组。

stats返回合约的主要信息：page_size，count，offset 和 page。他们满足的计算关系为：count = PAGE_SIZE * (page - 1) + offset

roll_over是内部函数，由它实际来创建LenthyLogger的actor class。[参见这里](https://github.com/alexxuyang/icp_course_H_1/blob/b17e7c5e33a87655c7bbe9389b502c4c645fba79/MyLogger.mo#L48)

您如果需要本地调试，建议将[PAGE_SIZE](https://github.com/alexxuyang/icp_course_H_1/blob/b17e7c5e33a87655c7bbe9389b502c4c645fba79/MyLogger.mo#L21)改成4，以达到创建多个actor class的效果。

下面是我在本地的一些测试配图


本地candid UI
![本地candid UI](https://github.com/alexxuyang/icp_course_H_1/blob/main/images/1.png)

第一次添加五个元素
![第一次添加五个元素](https://github.com/alexxuyang/icp_course_H_1/blob/main/images/2.png)

第二次添加八个元素
![第二次添加八个元素](https://github.com/alexxuyang/icp_course_H_1/blob/main/images/3.png)

使用view接口查看单一元素
![使用view接口查看单一元素](https://github.com/alexxuyang/icp_course_H_1/blob/main/images/4.png)

使用view接口查看跨越多个logger实例的日志
![使用view接口查看跨越多个logger实例的日志](https://github.com/alexxuyang/icp_course_H_1/blob/main/images/5.png)

使用view入参越界报错
![使用view入参越界报错](https://github.com/alexxuyang/icp_course_H_1/blob/main/images/6.png)

使用print_info在后台打印调试信息
![使用print_info在后台打印调试信息](https://github.com/alexxuyang/icp_course_H_1/blob/main/images/7.png)
