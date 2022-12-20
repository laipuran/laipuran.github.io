---
layout: post
title: C++ Socket 解决方案
date: 2020-05-03 14:26:10 +0800
---
###  1. inet_addr()函数过旧问题

在VS高版本(VS2021)里inet_addr()会报错，在这里我不推荐[关闭SDL检查](#4-关闭sdl检查不推荐)，而是使用 **inet_pton()** 或者 **inet_ntop()**
具体用法见
[inet_pton()百度百科](https://baike.baidu.com/item/inet_pton/)
[inet_ntop()百度百科](https://baike.baidu.com/item/inet_ntop/)

```c
inet_pton(地址系, "IP地址", (void*强制转换)&socket名称.sin_addr);
inet_ntop(地址系, "IP地址", (void*强制转换)&socket名称.sin_addr)
```
**实际上我也不知道这两者的差别**

完整代码

###  2. 服务器代码
服务器的主要思路就是：初始化 → 绑定服务器套接字 → 监听和连接 → 通信 → 清缓存和断开
```cpp
//Server
#include <iostream>
#include <WinSock2.h>
#include <WS2tcpip.h>

#pragma comment (lib, "ws2_32.lib")

using namespace std;

int main() {
    // 初始化套接字
    WSADATA wsaData;
    int err = WSAStartup(MAKEWORD(2, 2), &wsaData);
    if (err != 0) {
        cout << "初始化套接字失败！" << endl;
        system("pause");
        return 0;
    }
    else
        cout << "初始化套接字成功！" << endl;

    SOCKET serverSock = socket(PF_INET, SOCK_STREAM, 0);
    sockaddr_in serverAddr;
    memset(&serverAddr, 0, sizeof(serverAddr));
    serverAddr.sin_family = PF_INET;
    serverAddr.sin_port = htons(5000);
    
    inet_pton(PF_INET, "127.0.0.1", (void*)&serverAddr.sin_addr);
    //或者inet_ntop
	//重点,使用inet_addr在高版本VS会报错

    bind(serverSock, (SOCKADDR*)&serverAddr, sizeof(SOCKADDR));
    cout << "绑定套接字成功！" << endl;
    listen(serverSock, 20);
    sockaddr clientAddr;
    int size = sizeof(SOCKADDR);
    cout << "accept函数！" << endl;
    SOCKET clientSock = accept(serverSock, (SOCKADDR*)&clientAddr, &size);

    char buffer[30];
    memset(&buffer, '/0', sizeof(buffer));
    cout << "输入一句话：" << endl;
    cin >> buffer;
    send(clientSock, buffer, strlen(buffer) + sizeof(char), NULL);
    cout << "数据发送成功！" << endl;

    closesocket(clientSock);
    closesocket(serverSock);
    WSACleanup();
    system("pause");
    return 0;
}
```

###  3. 客户端代码
```cpp
//Client
#include <iostream>
#include <WinSock2.h>
#include <WS2tcpip.h>

#pragma comment (lib, "ws2_32.lib")

using namespace std;

int main() {
    WSADATA wsaData;
    int err = WSAStartup(MAKEWORD(2, 2), &wsaData);
    if (err != 0) {
        cout << "初始化套接字失败！" << endl;
        system("pause");
        return 0;
    }
    else
        cout << "初始化套接字成功！" << endl;
    SOCKET clientSock = socket(PF_INET, SOCK_STREAM, 0);
    sockaddr_in clientAddr;
    memset(&clientAddr, 0, sizeof(clientAddr));
    clientAddr.sin_family = PF_INET;
    clientAddr.sin_port = htons(5000);
    
    inet_pton(PF_INET, "127.0.0.1", (void*)&ClientAddr.s_addr);
    //或者inet_ntop
	//重点,使用inet_addr在高版本VS会报错
	
    printf("客户端发送请求\n");
    connect(clientSock, (SOCKADDR*)&clientAddr, sizeof(SOCKADDR));
    char buffer[MAXBYTE] = { 0 };
    recv(clientSock, buffer, MAXBYTE, NULL);

    cout << "接收服务器消息" << endl;
    cout << "服务器:" << buffer << endl;
    closesocket(clientSock);
    WSACleanup();
    system("pause");
    return 0;
}
```
###  4. 关闭SDL检查（不推荐）
在.cpp第一行前插入
```cpp
#define _WINSOCK_DEPRECATED_NO_WARNINGS
```
也可以解决。

<script src="https://utteranc.es/client.js"
        repo="laipuran/laipuran.github.io"
        issue-term="title"
        label="💬Comment"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>
