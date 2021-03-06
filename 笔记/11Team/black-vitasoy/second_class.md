## 抓取浏览器信息
![http请求头](https://github.com/DigBullTech-viewer/ctf_web/blob/master/src/black-vitasoy002.JPG)
![http响应头](https://github.com/DigBullTech-viewer/ctf_web/blob/master/src/black-vitasoy001.JPG)
## 在浏览器地址栏输入网站www.badu.com
总共是有五层然后发送信息到服务端:分别为应用层(http),传输层(tcp),网络层(ip),数据链路层(mac),物理层(0101011)
## 客户端
1. 客户端先查本地有无对应的IP地址,若找到则响应,无则请求上级DNS服务器,知道找到对应的IP地址
2. 首先是通过应用客户端发起HTTP请求:有包括请求包头和请求主体,其中包头的信息有:包括请求的方法（GET / POST）、目标url、遵循的协议（http / https / ftp…），返回的信息是否需要缓存，以及客户端是否发送cookie等。
3. 然后通过TCP传输报文,进行三次握手,即服务端先发送一个带有SYN标志的数据包给接收端,接收端收到数据包后，传回一个带有SYN/ACK标志的数据包以示传达确认信息。接收方收到后再发送一个带有ACK标志的数据包给接收端以示握手成功
4. 网络层IP协议查询MAC地址, IP协议的作用是把TCP分割好的各种数据包传送给接收方。而要保证确实能传到接收方还需要接收方的MAC地址，也就是物理地址。IP地址和MAC地址是一一对应的关系，一个网络设备的IP地址可以更换，但是MAC地址一般是固定不变的。ARP协议可以将IP地址解析成对应的MAC地址。当通信的双方不在同一个局域网时，需要多次中转才能到达最终的目标，在中转的过程中需要通过下一个中转站的MAC地址来搜索下一个中转目标
5. 找到对方的MAC地址后,就将数据发送到数据链路层传输
## 服务端
1. **服务端接收数据**,接收端的服务器在链路层接收到数据包，再层层向上直到应用层。这过程中包括在运输层通过TCP协议讲分段的数据包重新组成原来的HTTP请求报文。
2. **服务器响应请求**,服务接收到客户端发送的HTTP请求后，查找客户端请求的资源，并返回响应报文，响应报文中包括一个重要的信息——状态码。状态码由三位数字组成，其中比较常见的是200 OK表示请求成功。301表示永久重定向，即请求的资源已经永久转移到新的位置。在返回301状态码的同时，响应报文也会附带重定向的url，客户端接收到后将http请求的url做相应的改变再重新发送。404 not found 表示客户端请求的资源找不到。
3. **服务器返回相应文件**,请求成功后，服务器会返回相应的HTML文件。接下来就到了页面的渲染阶段了
