# sing-box 脚本自动 TLS 帮助说明

sing-box 脚本使用了 Caddy 实现自动配置 TLS。

## 介绍

Caddy 无敌好用！官网：https://caddyserver.com/

## 目录

- Caddy 配置目录：`/etc/caddy`
- 自定义配置目录：`/etc/caddy/sites`
- sing-box 脚本自动 TLS 配置目录：`/etc/caddy/laolitongxue`

## 更改自动 TLS 配置

你可以在 `/etc/caddy/laolitongxue` 目录找到自动 TLS 配置。一个域名会生成两个文件，一个是 `域名.conf`，另一个是 `域名.conf.add`。

请不要直接更改 `域名.conf` 文件。如果你想要自定义一些东西，请更改 `域名.conf.add` 文件，然后使用 `sb restart caddy` 重启 Caddy。

> 备注，如果使用了 sing-box 脚本设置更改伪装网站，`域名.conf.add` 文件会被重置。

## 提醒

请不要直接更改 `/etc/caddy/Caddyfile` 文件，如果你想要添加别的 Caddy 网站配置，请使用自定义配置。

## 自定义配置

为了方便你使用 Caddy，sing-box 脚本创建了一个目录用来给你放自定义配置。你可以在 `/etc/caddy/sites` 存放你另外的网站配置，注意后缀要为 `.conf`。

这里说的是 Caddy 的配置，不是让你把 html 之类的文件放到 `/etc/caddy/sites`。

## 证书目录

Caddy 自动申请了 SSL 证书；如果你有需要，可以直接使用。

保存在：`/root/.local/share/caddy/certificates/acme-v02.api.letsencrypt.org-directory`

此目录下有你配置的相关域名，打开相关域名的目录，就能找到证书相关文件，主要使用 `.crt` 和 `.key` 这两个文件，一个是证书一个是密钥。

## 其他

如果你觉得 Caddy 性能不好，可以使用 no-auto-tls 来自己配置 TLS 使用，详见：[sing-box 脚本 no-auto-tls 参数帮助说明](no-auto-tls.md)。

> 本文档基于开源项目 233boy/sing-box（GPL-3.0 License）的使用文档整理改写，去除广告与推广信息。
