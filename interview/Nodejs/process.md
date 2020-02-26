# process

## 标准流

`nodejs` 的`console.log` 是通过使用标准输出输入流实现的: `process.stdout` 、`process.stderr`.

## child_process

### spawn

usage: `child_process.spawn(command, [args]. [options])` .

    let child1 = spawn('node', ['test1.js', 'yanyongchao'], {
        stdio: ['pipe', 'pipe', 'pipe'], // 三个元素数组 下面会详解
        cwd: __dirname, 子进程工作目录
        env: process.env, 环境变量
        detached: true // 如果为true，当父进程不存在时也可以独立存在
    })

### stdio

这个参数决定了父子通讯的方式

1. `pip` 在父子间会打通一个通道,父进程可以通过`child.stdout.on('data')` 获取输出.
2. `process.stdout` , `process.stdin` ,`process.stderr` 这样的传值会让子进程的输入输出流直接输出到控制台
3. `ipc` :使用`p.on('message')` 语法获取信息输出.

### detached

`detached` 模式下,父进程的推出不会导致子进程的退出.

## Cluster

Cluster 是常见的 Node.js 利用多核的办法. 它是基于 child_process.fork() 实现的, 所以 cluster 产生的进程之间是通过 IPC 来通信的, 并且它也没有拷贝父进程的空间, 而是通过加入 cluster.isMaster 这个标识, 来区分父进程以及子进程, 达到类似 POSIX 的 fork 的效果.

## IPC(进程间通讯)

两个进程间进行数据交换的过程.

- 由于某些原因，应用自身需要采用多进程模式来实现。可能原因有：

某些模块因特殊原因要运行在单独进程中； 为加大一个应用可使用的内存，需通过多进程来获取多份内存空间。

- 当前应用需要向其它应用获取数据。

## 守护进程

守护进程是不依赖终端（tty）的进程, 不会因为用户退出终端而停止运行的进程.

nodejs开发守护进程的远离是父进程以`detached`模式`fork`一个子进程,然后退出父进程.此时子进程由`init`接管,成为孤儿进程.