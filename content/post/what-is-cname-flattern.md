+++
categories = ["开发", "中文"]
date = "2017-01-17T16:48:13+08:00"
description = ""
draft = true
tags = ["DNS", "开发", "运维"]
title = "什么叫 CNAME Flatten"

+++

最近搞 DNS，在云闪（人家正式的名字叫 Cloudflare 魂淡）看到一个叫 CNAME Flatten 的功能。新鲜，没见过。一查不得了，中文资料近乎没有，这搞毛啊。我就占个坑解释下这东西是啥。

# 解决的问题：

1. A 记录只能指向单个 IP。无法有效利用已有的 CDN 网络。比方说，Google有这么多服务器，你加 A 记录的话只能指向某一个 IP，其他的服务器永远访问不到，多尴尬（用 CNAME 可解）
2. 可惜，CNAME 记录不能应用于根域名。你可以给比方说：你可以给[www.parisqian.com](https://www.parisqian.com) 加 CNAME 到 [qiansen1386.github.io][1] 但不能把 [parisqian.com](https://parisqian.com) 也指向 [qiansen1386.github.io][1]。这将导致 @parisqian.com 的 MX 记录失效。（故而 DNS 标准形成时候的几个 RFC 都不允许这种做法）（在 `www` 子域名上应用 CNAME 可解）
3. 很不易于推广嘛。你怎么跟你的用户解释，为什么打 `www` 和不打 `www` 打开的网站完全不同？并且叮嘱网友一定要加 `www`。_(:з」∠)_

#CNAME Flatten 可解！

CNAME Flatten 会解析并把你的 CNAME 记录解析为一系列 A 记录的缓存，赛高得死🙌。

```
$ dig example.com

QUESTION SECTION:
;example.com.   IN   A

;; ANSWER SECTION:
example.com.   299   IN   A   162.159.255.115
example.com.   299   IN   A   162.159.254.115
example.com.   299   IN   A   162.159.252.116
example.com.   299   IN   A   162.159.253.116
example.com.   299   IN   A   162.159.253.115
```
栗子抄自 Cloudflare

#附录#
\#1 CNAME是啥？别名解析，也就是从一个域名指向另一个域名。由此可以形成一个解析链条。并最终得到一个具体的 A 或 AAAA 记录（即 IP）。

\#2 **最常见的资源记录类型有**

- A记录（主机记录）：RFC 1035定义，A记录是用于名称解析的重要记录，它将特定的主机名映射到对应主机的IP地址上。
- CNAME记录（别名记录）: RFC 1035定义，CNAME记录用于将某个别名指向到某个A记录上，这样就不需要再为某个新名字另外创建一条新的A记录。
- AAAA记录（IPv6主机记录）: RFC 3596定义，与A记录对应，用于将特定的主机名映射到一个主机的[IPv6](https://zh.wikipedia.org/wiki/IPv6)地址。

（来源[域名系统 - 维基百科](https://zh.wikipedia.org/wiki/%E5%9F%9F%E5%90%8D%E7%B3%BB%E7%BB%9F)）

\#3 **DNS 的几个主要 RFC 的生成年份**

- [http://tools.ietf.org/html/rfc1034](http://tools.ietf.org/html/rfc1034) November, 1987
- [http://tools.ietf.org/html/rfc1035](http://tools.ietf.org/html/rfc1035) November, 1987
- [http://tools.ietf.org/html/rfc1912](http://tools.ietf.org/html/rfc1912) February, 1996

（来源[CNAME Flattening: RFC-compliant support for CNAME at the root - CloudFlare Support](https://support.cloudflare.com/hc/en-us/articles/200169056-CNAME-Flattening-RFC-compliant-support-for-CNAME-at-the-root)）

[1]: qiansen1386.github.io  "qiansen1386.github.io"