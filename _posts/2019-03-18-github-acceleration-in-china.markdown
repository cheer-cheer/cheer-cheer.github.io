---
layout: post
title:  "GitHub 中国境内访问加速"
date:   2018-03-18 23:34:05 +0800
categories: github IT 墙
---

因为一些众所周知的深层原因，GitHub 在境内受到 DNS 污染，访问速度受到了极大影响。通常的解决方法是：找那些没有受到污染的 IP，配置到 hosts 文件中。但是这种 IP 时效性比较高，网上的文章不会及时更新，配置后效果不很理想。其实，完全不需要百度，可以直接使用 `nslookup` 命令去自动解析域名来查找这些 IP。

```bash
nslookup -vc github.com 8.8.8.8
```

有空的话，可以写个脚本，自动选取最佳的 IP 填到 hosts 文件里 ^_^