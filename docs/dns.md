# sing-box 脚本 DNS 设置

sing-box 脚本可以非常快速设置 DNS，一键配置 DNS DOH 加密以及屏蔽色情网站，或者自定义 DNS。

## 前言

DNS 是联网的开始，有些时候上不了网，或许就是你的 DNS 崩了，不过这里暂不讨论客户端 DNS。

默认情况下，DNS 是通过 53 端口 UDP 协议出去查询的，简单说就是，查询的过程中是透明的、没有加密的，VPS 服务商或者网络提供者可以看到你查询了什么域名。所以如果在乎隐私，使用 DNS DOH 方式来查询是非常有必要的，使用 DOH 方式就不用担心别人能看到你查询了哪些域名。

sing-box 脚本同时提供 DNS IP 方式、DNS DOH（HTTP/3）方式，你也可以自定义 DNS。

## 设置 DNS

输入 `sb dns`（或 `sing-box dns`）即可选择相关 DNS：

- `set` 选项：自定义 DNS
- `none` 选项：不配置任何 DNS

## google

快速设置 Google DNS：`sb dns 88`

快速设置 Google DNS DOH：`sb dns gg`

## cloudflare

快速设置 Cloudflare DNS：`sb dns 11`

快速设置 Cloudflare DNS DOH：`sb dns cf`

## nosex

快速设置 Cloudflare Family DNS DOH：`sb dns nosex`

备注，使用此方式将无法打开成人网站（提供给有特殊需求的时候使用）。

## set

快速自定义 DNS 使用 9.9.9.9：`sb dns set 9.9.9.9`

快速自定义使用 ADGUARD DNS DOH：`sb dns set https://dns.adguard-dns.com/dns-query`

使用 `sb dns set` 可以手动输入 DNS 值，或者 `sb dns set 1.1.1.1` 直接指定使用 1.1.1.1 作为 DNS，后面的 1.1.1.1 可以自定义成任何你喜欢的 DNS。

## none

如果你出现任何问题，请使用 `sb dns none` 来重置 DNS 配置；或者如果你想要 sing-box 走系统 DNS，也使用此命令。

## 结束

理论上只要记得 `sb dns nosex` 这个命令就行。

啊这，别手残自定义使用国内的 DNS。

> 本文档基于开源项目 233boy/sing-box（GPL-3.0 License）的使用文档整理改写，去除广告与推广信息。
