# CLAUDE.md

本文件为 Claude Code (claude.ai/code) 在此仓库中工作时提供指导。

## 概述

这是《TCP/IP 网络编程》一书的学习笔记仓库，包含按章节组织的 Markdown 笔记和配套的 C 语言示例代码，演示套接字编程的核心概念。

**开发环境**：Ubuntu 18.04 LTS，gcc 7.3.0

**仓库地址**：https://github.com/riba2534/TCP-IP-NetworkNote

## 目录结构

```
ch01/    - 第 1 章：理解网络编程和套接字
ch02/    - 第 2 章：套接字类型与协议设置
ch03/    - 第 3 章：地址族与数据序列
ch04/    - 第 4 章：基于 TCP 的服务端/客户端（1）
ch05/    - 第 5 章：基于 TCP 的服务端/客户端（2）
ch06/    - 第 6 章：基于 UDP 的服务端/客户端
ch07/    - 第 7 章：优雅地断开套接字的连接
ch08/    - 第 8 章：域名及网络地址
ch09/    - 第 9 章：套接字的各种选项
ch10/    - 第 10 章：多进程服务器端
ch11/    - 第 11 章：进程间通信
ch12/    - 第 12 章：I/O 复用
ch13/    - 第 13 章：I/O 复用（2）
ch14/    - 第 14 章：多播与广播
ch15/    - 第 15 章：套接字和标准 I/O
ch16/    - 第 16 章：关于 I/O 流分离的其他内容
ch17/    - 第 17 章：优于 select 的 epoll
ch18/    - 第 18 章：多线程服务器端的实现
ch24/    - 第 24 章：制作 HTTP 服务器端
```

每个章节目录包含：
- `README.md` - 章节笔记（理论 + 习题）
- `.c` 文件 - 示例代码

项目根目录包含：
- `images/` - 所有章节的图片资源（统一存放）

## 编译和运行

所有示例都是独立的 C 程序，使用 gcc 编译：

```bash
# 编译服务端示例
gcc hello_server.c -o hserver

# 编译客户端示例
gcc hello_client.c -o hclient

# 运行服务端（需要端口号参数）
./hserver 9190

# 运行客户端（需要 IP 地址和端口号）
./hclient 127.0.0.1 9190
```

多线程示例（第 18 章）需要链接 pthread 库：
```bash
gcc thread1.c -o tr1 -lpthread
```

## 内容规范

修改此仓库内容时需注意：

1. **专注于 Linux 平台**：本仓库专门讲解 Linux 套接字编程。Windows 平台相关内容标记为"暂略"。

2. **保持中文术语一致性**：
   - IPv4/IPv6（不要用 IPV4/IPV6）
   - "接收"（receive）不要写成"接受"
   - "连接"（connection）不要写成"链接"

3. **章节更新流程**：根目录 README.md 包含所有 19 个章节的合并内容。更新内容时，先修改子目录中对应章节的 README.md，然后合并到根 README.md。

4. **代码引用格式**：引用示例代码时使用相对路径，不加章节前缀（例如用 `[hello_server.c](hello_server.c)` 而不是 `[hello_server.c](ch01/hello_server.c)`）。

5. **图片引用格式**：所有图片统一存放在根目录 `images/` 下。在 README.md 中引用图片时使用统一路径 `images/文件名.png`（无论是根目录还是子目录的 README.md）。

## 涵盖的核心套接字编程概念

- **TCP vs UDP**：面向连接（SOCK_STREAM）vs 无连接（SOCK_DGRAM）
- **服务端生命周期**：socket() → bind() → listen() → accept() → read/write → close()
- **客户端生命周期**：socket() → connect() → read/write → close()
- **I/O 模型**：阻塞、非阻塞、I/O 复用（select、epoll）
- **并发方式**：多进程（fork）、多线程（pthread）
- **高级主题**：半关闭（shutdown）、套接字选项、多播/广播
