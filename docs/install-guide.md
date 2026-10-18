# sing-box 一键搭建教程

搭建 sing-box 看这篇教程就够了！从购买 VPS 到 SSH 登录，再到使用 sing-box 一键安装脚本配置，一步一步完成，确保你可以百分百成功搭建 REALITY、Hysteria2、TUIC、Trojan、VLESS-WS-TLS 等协议使用。

本教程纯文字步骤，无截图。

## 前言

本教程完完全全是为新手准备的：从购买 VPS，到使用 SSH 客户端登录，再到使用 [sing-box 一键安装脚本](usage.md) 完成服务器端配置。哪怕你是第一次接触这些陌生的东西，照着步骤做即可。

## 流程总览

1. 购买一台 VPS（想要搭建代理服务，就必须要拥有一台 VPS）
2. 获取 VPS 信息（VPS IP 地址、root 用户密码、SSH 端口）
3. 安装 SSH 客户端（例如 Xshell）
4. 登录 VPS
5. 安装 sing-box（极速安装，全程自动）
6. 安装完成，使用客户端测试连接
7. 进阶玩法（配置 VLESS-REALITY、TUIC、Trojan、Hysteria2、VMess-WS-TLS 等）

## 购买一个 VPS

想要搭建代理服务，拥有一台 VPS 是必需的。选择 VPS 时重点关注：

- **线路**：到国内晚高峰的稳定性比配置更重要；香港、新加坡、日本等优化线路到晚上一般不会怎么炸，普通线路晚高峰可能会很慢。
- **系统**：推荐 Ubuntu 22.04（本脚本对 CentOS 支持较差）。
- **付款方式**：按需选择，主流商家基本都支持支付宝。

> 如果你只是单纯的需求，也可以直接购买机场服务，不用自己搭建，省心省力。

## 获取 VPS 信息

购买完成后，在 VPS 商家的管理面板可以看到三样必需要有的信息：

- **IP 地址**
- **root 用户密码**（部分商家重装系统后才会生成）
- **SSH 端口**（部分商家不是默认的 22）

如果商家面板没有直接给密码，通常需要先重装一次系统（选择 ubuntu-22.04-x86_64），重装完成后面板会显示新的 root 密码和 SSH 端口，**务必记下来**。

## 安装 SSH 客户端

以 Xshell 为例（其他 SSH 客户端如 Termius、Windows Terminal 自带的 ssh 也可以）：

1. 到 Xshell 官网下载 Home/School 免费版本并安装，一路默认下一步即可。
2. 安装完成后首次打开需要输入名称和邮箱完成免费授权注册。

## 登录 VPS

1. 在 Xshell 中新建一个会话，主机填 VPS 的 IP 地址，端口填 SSH 端口。
2. 切换到「用户身份验证」，用户名填 root，密码填你的 root 密码，然后确定。
3. 选择连接；如果提示 SSH 安全警告，选择「接受并保存」。
4. 看到命令行提示符即登录成功。

## 安装 sing-box

登录后，在终端执行下面命令（在 Xshell 界面按 Shift + Insert 即可粘贴）：

```bash
bash <(wget -qO- -o- https://github.com/laolitongxue/sing-box/releases/latest/download/install.sh)
```

## 安装完成

命令执行后没有错误提示的话，会显示安装耗时（绝大多数情况下 15 秒内完成），并自动创建一个 VLESS-REALITY 配置。复制输出的 URL 到客户端软件（例如 v2rayN）测试是否正常使用。

如果无法正常使用，请尝试 `sb add ss auto auto aes-256-gcm` 添加一个 SS 再测试。

## 管理面板

输入 `sb`（或 `sing-box`）回车即可打开管理面板；不想执行任何功能时直接按 Enter 退出。

## 无法使用排查

无法使用一般是两种情况：一是无法连接上端口，二是客户端内核支持有问题。

1. 如果你的 VPS 有外部防火墙（云控制台安全组），请确保已开放端口。
2. 打开 https://tcp.ping.pe/ ，写上 `VPS IP:端口`（示例 `1.1.1.1:443`）测试；显示 successful 证明端口能连接，failed 则是连不上。
3. 可以用 `sb ip` 查看 VPS IP。
4. 关闭系统防火墙：`systemctl stop firewalld; systemctl disable firewalld; ufw disable`，然后重新测试端口。
5. 端口通了还不行，用 `sb add ss auto auto aes-256-gcm` 添加一个 SS 测试；能正常使用说明服务端没问题，问题在客户端：
   - 客户端内核太旧，更新客户端 sing-box 内核与服务器端保持一致
   - 尝试设置 VMessAEAD
   - 某些客户端需要把额外 id（alterid）填为 0
   - 换不同客户端测试（v2rayN、v2rayNG 等）

## 常用协议快速实现

- **VLESS-REALITY**：`sb add reality` 回车即可
- **Hysteria2**：`sb add hy` 回车即可
- **TUIC**：`sb add tuic` 回车即可
- **VMess-WS-TLS / VLESS-WS-TLS / Trojan-HTTPUpgrade-TLS**：需要一个能正常解析的域名，服务器执行 `sb add wss`（或 `sb add vws`、`sb add thu`）回车，输入域名即可
- 打开 BBR 优化：`sb bbr`

哪个传输协议好？

- 心中无杂念，用 TCP
- VPS 速度不好，用 TUIC / Hysteria2
- 想要最抗封锁，用 VLESS-REALITY

## 其他

请勿违反所在国家或地区的法律法规，否则后果自负。

> 本文档基于开源项目 233boy/sing-box（GPL-3.0 License）的使用文档整理改写，去除广告、推广信息与带第三方 Logo 的截图。
