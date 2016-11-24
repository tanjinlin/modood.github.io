# dns

```
dns.getServers()                                  返回一个用于当前解析的 IP 地址的数组的字符串
dns.setServers(servers)

dns.lookup(hostname[, options], callback)         将域名（比如 'google.com'）解析为第一条找到的记录A(IPV4)或AAAA(IPV6)
dns.lookupService(address, port, callback)        使用 getnameinfo 解析传入的地址和端口为域名和服务。

dns.reverse(ip, callback)

dns.resolve(hostname[, rrtype], callback)         将一个域名（如 'google.com'）解析为一个 rrtype 指定记录类型的数组。
dns.resolve4(hostname[, options], callback)       和 dns.resolve() 类似，但仅能查询 IPv4
dns.resolve6(hostname[, options], callback)       和 dns.resolve() 类似，但仅能查询 IPv6
dns.resolveCname(hostname, callback)              和 dns.resolve() 类似，但仅能进行别名记录查询 (CNAME记录)
dns.resolveMx(hostname, callback)                 和 dns.resolve() 类似，但仅能查询邮件交换(MX 记录)
dns.resolveNaptr(hostname, callback)
dns.resolveNs(hostname, callback)                 和 dns.resolve() 类似，但仅能进行域名服务器记录查询(NS 记录）
dns.resolveSoa(hostname, callback)                和 dns.resolve() 类似，但仅能查询权威记录(SOA 记录）
dns.resolveSrv(hostname, callback)                和 dns.resolve() 类似，但仅能进行服务记录查询 (SRV 记录）
dns.resolvePtr(hostname, callback)
dns.resolveTxt(hostname, callback)                和 dns.resolve() 类似，但仅能进行文本查询 (TXT 记录）
```

