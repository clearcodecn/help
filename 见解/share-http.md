### 粗略理解 `HTTP` 协议到实际业务的应用

* 张梦金


----

#### 访问一个网站到底发生了什么 ? 

```
wget https://www.baidu.com/ 
```

![http协议](http-bs.jpg)


---

#### part1. TCP服务端

```
func main()  {
	l , _ := net.Listen("tcp", ":8080")
	conn , _ := l.Accept()
	b := make([]byte,1024)
	n, _ := conn.Read(b)
	fmt.Println(string(b[:n]))
	conn.Write([]byte("HTTP/1.1 200 OK\r\n\r\n hello world"))
	conn.Close()
	l.Close()
}
// 打印数据
GET / HTTP/1.1	请求方法  路劲 协议版本\r\n
User-Agent: Wget/1.19.5 浏览器头：浏览器类型\r\n
Accept: */*		接受格式
Accept-Encoding: identity  接受编码
Host: localhost:8080   请求的域名
Connection: Keep-Alive  连接保持策略
```

----

#### part1. TCP服务端
* 响应
```
➜  ~ cat index.html
 hello world
```
* 实际发送
```
HTTP/1.1 200 OK\r\n\r\n hello world
```

--- 

#### part1. TCP服务端

##### 初步结论

* 一个请求需要建立一次`TCP`连接
* 请求完了，该连接需要关闭
* 该服务端代码只能执行一次请求
* 很多问题可以根据这段请求与响应代码去判断到底是服务端代码错误还是客户端代码错误, 如：httpCode异常，请求发出却没有响应数据，服务器拒绝连接，请求格式错误 
* 只要符合http报文格式，一切皆可自定义

---

#### part2. 服务端并发与优化

```
var resp = []byte("HTTP/1.1 200 OK\r\nContent-Length: 11\r\n\r\nhello world")
func main()  {
	l , _ := net.Listen("tcp", ":8080")
	defer l.Close()
	for {
		conn , _ := l.Accept()
		go func() {
			defer conn.Close()
			for {
				b := make([]byte,1024)
				_, err := conn.Read(b)
				if err != nil {
					break
				}
				conn.Write(resp)
			}
		}()
	}
}
```

---- 

#### part2. 服务端并发与优化

##### 进一步结论
* keep-alive 实现tcp长连接，减少握手
* 一个tcp连接，http请求是串行的，不同的tcp连接,请求是并行的.
* keep-alive策略. 如连接3分钟没有活动就断开. 
* 服务器达到了最大tcp连接底层是尝试等待获取资源进行新的连接

---- 

#### part2. 服务端并发与优化

![net包实现原理](tcp-1.png)


---

#### part3. 实际应用场景

1. 共享内存与锁
2. 负载均衡
3. 使用缓存，提高`IO`效率
4. 精简请求次数以及请求/响应数据量(带宽)
5. 谨慎操作全局变量


#### 锁

```
sync.Mutex 一个时间片只有一个goroutine获得该资源的访问权
sync.RWMutex 随便读，除非 RLock, 写时锁, 性能好

```
--- 


### 总结

* HTTP 协议大致原理
* 开发调试错误判断
* 服务端优化
* 一切皆IO

---

* tip

> 传输
```
if tcp三次握手 {
    go while(true) {
        client  --request --> server --> handler(req,*resp)
        client  <--response <-----------------|
        if timeout || clientClosed {
            break
        }
    }
}
```
> 数据
```
client request length = Header + Body
server response length = Header + Body 
```

--- 
# THANK YOU :smile:























