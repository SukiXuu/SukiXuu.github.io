---
author: "Suki Xuu"
title: "个人网站搭建3 --Custom Domain"
date: "2025-01-23"
description: "让在github pages上搭建的个人网站，使用个人域名"
cntags: ["Web Build", " Domain Name"]
ShowToc: false
ShowBreadCrumbs: false
---

使用个人域名。

<!--more-->
### 域名解析
- 比如我的域名是sukixuu.click，使用域名服务商的DNS解析功能，将`sukixuu.click`域名指向GitHub Pages的IP地址。 
添加一条A记录，value为**GitHub Pages的IP地址**，如:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

- 将子域名`www.sukixuu.click`指向`sukixuu.github.io`。
添加一条CNAME记录，value为`sukixuu.github.io`。

### GitHub 创建CNAME reord，用于将我的域名指向GitHub Pages
在GitHub Repo的Settings中，Pages section下找到Custom Domain，输入`sukixuu.click`，点击Add，GitHub会自动创建一条CNAME记录，用于将sukixuu.click指向GitHub的服务器。

**Enforce HTTPS 选项**启用，GitHub 会自动为你生成并配置 SSL 证书。

### 验证域名解析
- 打开浏览器，输入`http://sukixuu.click`，如果看到GitHub Pages的默认页面，则说明域名解析成功。
- 如果看到的是404页面，则说明域名解析失败，请检查域名解析是否正确。



--- 
DNS记录（DNS Records）
DNS（域名系统）用来将域名与互联网资源（如IP地址、邮件服务器等）进行关联的条目。DNS记录对于确保互联网应用能够正确地访问目标资源至关重要。以下是几种常见的DNS记录类型：

- A记录（Address Record）：将域名指向一个特定的IPv4地址。
- AAAA记录（IPv6 Address Record）：将域名指向一个特定的IPv6地址。
- CNAME记录（Canonical Name Record）：将域名指向另一个域名，通常用于将子域名指向主域名。

- MX记录（Mail Exchange Record）：指定邮件服务器的域名。

- TXT记录（Text Record）：为域名添加说明文字。
- PTR记录（Pointer Record）：将IP地址指向域名。
- SRV记录（Service Record）：记录特定服务的服务器域名和端口号。
- SPF记录（Sender Policy Framework Record）：记录允许发送邮件的IP地址范围。  **不推荐使用**
- NAPTR记录（Name Authority Pointer Record）：记录域名的NAPTR记录。由 DDDS 应用程序使用。
- CAA记录（Certification Authority Authorization Record）：记录域名的CA机构颁发的SSL证书。

- **NS记录（Name Server Record）：指定域名服务器的域名。**
- DS记录（Delegation Signer Record）：记录子域名的DNSKEY记录。委派签名者，用于为 DNSSEC 建立信任链。

- TLSA记录（TLS Authentication Record）：记录域名的TLS证书信息。
- SSHFP记录（SSH Fingerprint Record）：记录SSH服务器的公钥指纹。
- HTTPS记录（HTTP Secure Record）：记录域名的HTTPS证书信息。
- SVCB记录（Service Binding Record）：记录域名的DNS-Based Service Discovery记录。 为访问服务端点提供可扩展的配置信息。

- SOA记录（Start of Authority Record）：记录域名的SOA记录。

