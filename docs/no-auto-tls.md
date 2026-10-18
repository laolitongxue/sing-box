# sing-box 脚本 no-auto-tls 参数帮助说明

如果你想要手动配置 TLS，请使用 no-auto-tls 参数来添加配置，例如你想要用 NGINX 实现 TLS。

## 前言

考虑到有些人不方便使用 Caddy 实现自动 TLS，比如已使用 NGINX 跑了自己的博客，又或者觉得 Caddy 性能不够好之类。sing-box 脚本自带了一个 no-auto-tls 参数，可以让你非常方便地手动配置 TLS。

## 备注

此处说的手动配置 TLS，指的是使用 WEB 程序转发 ws/h2/httpupgrade 流量到 sing-box。

## 添加一个配置

使用 `sb no-auto-tls` 添加一个配置。

可以在 no-auto-tls INFO 找到端口和路径。有了端口和路径参数，你就可以自己来手动配置 TLS，将相关的路径流量转发到 `127.0.0.1:端口` 即可。

VLESS-WS-TLS 协议可以参考 XTLS/Xray-examples 仓库中的 VLESS-WSS-Nginx NGINX 配置模板（https://github.com/XTLS/Xray-examples ）。

其他配置模板？都手动了，你手动一下吧。

## 提醒

no-auto-tls INFO 这个配置信息可以在使用 `sb info tls` 指令查看配置的时候自动显示；或者你也可以使用 `sb debug tls` 指令来查看，你可以找到 port 和 path 相关的信息。

## 缺点

都说了嘛，手动。所以如果你改了路径之类，又得自己来手动配置一次。

## 懂的都懂

不要好奇为什么显示配置的时候端口会是 443，而 no-auto-tls INFO 下面又是不同的端口。

> 本文档基于开源项目 233boy/sing-box（GPL-3.0 License）的使用文档整理改写，去除广告与推广信息。
