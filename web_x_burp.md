### burpsuite代理HSTS请求(macOS)

* 解决问题：burpsuite无法拦截某些https的请求，浏览器报错信息为 `ERR_SSL_VERSION_OR_CIPHER_MISMATCH.协议不受支持。`
  * 1.证书 `project options` - `SSL` 将`default`改为`Use custom protocols and ciphers`
  * 2.系统导入burpsuite的证书 访问 http://burp/cert 下载证书,打开mac的钥匙串访问`keychain`，导入证书并且修改`PortSwigger CA`为始终信任。

最终效果：
可正常使用burp抓取HSTS请求,浏览器显示信任该证书。

### Burpsuite - Macros

Brupsuite的Macros(宏)是一个预先定义好的HTTP请求序列，这个序列中可以包含一个或多个HTTP请求。

在Burpsuite的会话管理规则`Session Handling Rules`中使用Macros实现自动化

* 作用1 利用宏实现自动登录 保证cookie的有效性
  * 利用宏实现无验证码时的自动登录 从而保证cookie的有效性 所以后续扫描请求会正常执行
  * 可保证Intruder多次发送请求的有效性
* 作用2 提取某些值
  * 发送 HTTP请求1 获取 响应1 中的某些值(如CSRF Token)，把它作为 HTTP请求2 中的参数

参考 [Burpsuite中宏的使用 - FreeBuf](https://www.freebuf.com/articles/web/156735.html)

### burpsuite扩展 - bypassWAF

BApp安装bypassWAF后，

在burp的选项卡`Project options` - `Session Handling Rules` - `Rules Actions` - `Add`-`Invoke a Burp Extension` 选择`bypassWAF`

在`scope`里指定：工具范围 url范围 参数范围

这里只需要在`URL scope`里增加一个`Any`即可

### burpsuite扩展 - 检测nginx alias错误配置

alias traversal via NGINX misconfiguration

[PortSwigger/nginx-alias-traversal](https://github.com/portswigger/nginx-alias-traversal)

### burpsuite扩展 - NoPE Proxy

安装：

[summitt/Burp-Non-HTTP-Extension: Non-HTTP Protocol Extension (NoPE) Proxy and DNS for Burp Suite.](https://github.com/summitt/Burp-Non-HTTP-Extension)

使用参考：

[Burpsuite抓取非HTTP流量 - FreeBuf](https://www.freebuf.com/articles/network/158589.html)
