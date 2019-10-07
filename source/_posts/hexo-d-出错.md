---
title: hexo d 出错
date: 2019-10-03 17:10:34
tags: hexo 
categories:  
    - hexo 
comments: true
---

> Connection reset by 13.229.188.59 port 22
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
FATAL Something's wrong. Maybe you can find the solution here: https://hexo.io/docs/troubleshooting.html
Error: Connection reset by 13.229.188.59 port 22
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

    at ChildProcess.<anonymous> (D:\chacha-z.github.io\node_modules\hexo-util\lib\spawn.js:37:17)
    at ChildProcess.emit (events.js:198:13)
    at ChildProcess.cp.emit (D:\chacha-z.github.io\node_modules\cross-spawn\lib\enoent.js:40:29)
    at maybeClose (internal/child_process.js:982:16)
    at Socket.stream.socket.on (internal/child_process.js:389:11)
    at Socket.emit (events.js:198:13)
    at Pipe._handle.close (net.js:606:12)


<!--more-->

在执行备份（备份失败）（git add .\git commit -m "..."\git push origin hexo）后出现此问题

1. 试过“确保 ssh 正常，hexo-deploy-git 插件正常的情况下删除. deploy_git 文件夹就好了”，前一两次成功，后来又挂了
2. 试过“在windows防火墙设置22端口”，没用
3. 连手机热点，成功。？？？防火墙？