#  微服务架构服务

## 优点 
 1. 职责单一
 2. 轻量级通信(借助rpc协议)
 3. 独立性
 4. 扩展性强, 迭代开发 
## 缺点
1. 运维成本高
2. 分布式复杂
3. 接口成本高
4. 重复性劳动
5. 业务分离困难
   
# RPC 协议
* remote procedurecall Call Protocol 
  * 向调用本地函数一样调用远程数据
  * 通过rpc协议传输函数名,传递参数.调用远端函数,得到返回值.
 * 为什么微服务使用PRC
   * 跨进程通信
   * 跨语言通信
  
# RPC入门
## Socket网络通信
* server端: 
  * net.listen() -> listener
  * listener.Accept -> conn 
  * conn.Read(), conn.Write()
  * conn.Close(), listener.Close()
* client端:
  * net.Dial() -> conn
  * conn.Write()
  * conn.Read()
  * conn.Close()

## RPC使用步骤
* 服务端
  * 注册rpc服务对象. 给对象绑定方法(1.定义类, 2 绑定类方法)
  ```
  rpc.RegisterName("服务名", 回调对象)
  ```
  * 创建监听器
  ```
  net.Listen()
  ```
  * 建立连接
  ```
  listener.Accept()
  ```
  * 将连接绑定rpc服务.
  ```
  rpc.ServeConn(conn)
  ```
* 客户端
  * 用RPC连接服务器 
  ```
  conn, err := rpc.Dial()
  ```
  * 调用远程函数
  ```
  conn.Call("服务名.方法名", 传入参数, 传出参数)
  ```