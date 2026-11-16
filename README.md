# evilgod.loc.cc 落地页（域名保活用）

## 这个仓库是干什么的

给免费域名 **`evilgod.loc.cc`** 提供一个能打开、有有效证书的落地页，
纯粹是为了通过 Yunamo 的**域名健康检查**，防止域名被平台自动暂停/回收。

- 域名来源：Yunamo（NodeLoc 社区）每月 16 号免费 `.loc.cc` 二级域名
- 注册时间：2026-11-16，优惠码 `FREENOV2026`，**终身注册**（有效期到 2126-11-16）
- 订单号：`ORD179484198026fdf61f1a`，实付 NL0.00

## 为什么要这么绕

Yunamo 的健康检查会验证：`@` 根域 HTTP 可达 + SSL 证书有效 + DNS 解析正常。
连续不健康 **7 天**就会被暂停。

坑点：Yunamo 的 **CNAME 展平（LUA 记录）有 DNSSEC 签名缺陷**，
严格验证 DNSSEC 的解析器（签发证书的 CA 就是）会 SERVFAIL，导致证书签不下来。
Cloudflare Pages 强制要 CNAME，所以卡死。

**GitHub Pages 根域用 A 记录**（185.199.108.153 / 109.153 / 110.153 / 111.153），
A 记录实测能正常通过 DNSSEC，所以证书能签下来。这就是本仓库存在的原因。

## 部署结构

- 本仓库开 GitHub Pages（master 分支根目录），绑定自定义域 `evilgod.loc.cc`（靠根目录 `CNAME` 文件）
- `index.html` 是落地页，只要能返回 200 即可
- Yunamo 侧 `@` 记录配 4 条 A 记录指向 GitHub Pages IP

## 相关账号/位置

- GitHub 账号：`z1926401461-evil`
- Yunamo 账号：`z13668846073@gmail.com` 登录，域名 id `15114`
- 详细排障过程见本地日志 `2026-11-16.md`
