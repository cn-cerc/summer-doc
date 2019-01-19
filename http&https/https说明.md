# https说明

### HTTPS

HTTPS = HTTP + SSL，是 HTTP 基于 SSL 协议的网站加密传输协议，网站安装 SSL 证书后，使用 HTTPS 加密协议访问，可激活客户端浏览器到网站服务器之间的"SSL 加密通道"(SSL 协议)，实现高强度双向加密传输，以保护传输数据的隐私性与完整性。

### SSL

SSL（Secure Sockets Layer）即安全套接层，利用数据加密 (Encryption) 技术，可确保数据在网络上传输过程中不会被截取。SSL 协议位于 TCP/IP 协议与各种应用层协议之间，为数据通讯提供安全支持。

### SSL 证书

SSL 证书就是遵守 SSL 协议的服务器数字证书，由受信任的数字证书颁发机构CA颁发，具有服务器身份验证和数据传输加密等功能。

### CA

数字证书授权机构 （CA，Certificate Authority） 是负责发放和管理数字证书的权威机构。

### RSA

RSA 公钥加密算法是 1977 年由 Ron Rivest、Adi Shamir、Leonard Adleman 一起提出的，它是第一个能同时用于加密和数字签名的算法，从提出到现今经历了各种攻击的考验，能够抵抗到目前为止已知的绝大多数密码攻击，已被 ISO 推荐为公钥数据加密标准。

### ECC

ECC（Elliptic Curves Cryptography，椭圆曲线加密算法）也是一种公钥加密算法，与主流的 RSA 算法相比，ECC 算法可以使用较短的密钥达到相同的安全程度，其安全性更高、处理速度更快。

### CDN

CDN（Content Delivery Network，内容分发网络）距用户仅有"一跳"(Single Hop)之遥，依靠部署在各地的边缘服务器，使用户就近获取所需内容，降低网络拥塞，提高用户访问响应速度和命中率。

## 获取证书

升级HTTPS的首要条件就是要获得CA证书

CA证书可以跟证书机构直接购买，或者从代理商处购买

当然也可以自己生成证书，然而并不在浏览器的信任列表

国内部分的云服务厂商在购买其产品后可以申请一定数量的免费证书。

比如如阿里云的每个帐号可以免费申请20个由 `Symantec` 颁发的 `DV SSL` 证书

部署证书的一般步骤如下：

1. 购买证书
2. 身份认证
3. 安装证书

购买证书类型不同，身份认证流程也不同

证书收费策略根据认证级别和适用范围有所不同

## 证书分类

### 按认证级别分类

**域名认证（DV SSL）**

Domain Validation
    
申请流程简单，认证级别最低，可以验证申请人对域名的所有权

客户端验证成功后，一般会在浏览器地址栏显示一把锁

**组织认证（OV SSL）**

Organization Validation
    
申请流程复杂，认证级别较高，可以验证域名及组织的合法性

`OV SSL` 提供加密功能，对申请者做严格的身份审核验证，提供可信身份证明

`增强型OV SSL`(支持ECC椭圆曲线算法)，提供站点加密功能，需要核验组织注册信息，证书中显示组织名称

**扩展认证（EV SSL）**

Extended Validation
    
申请时申请人必须通过严谨的扩展验证流程，认证级别最高。
    
客户端验证成功后，会浏览器地址栏会显示公司名

`EV SSL`提供加密功能，对申请者做最严格的身份审核验证，提供最高度可信身份证明，提供浏览器绿色地址栏

`增强型EV SSL`(支持ECC椭圆曲线算法)，提供站点加密功能，浏览器绿色地址栏显示组织信息强化信任

### 按适用范围分类

**单域名SSL**

证书只能用于一个网站
    
example.com的证书将不能用于www.example.com

**多域名SSL**

证书可以用于多个网站
    
用于www.example.com证书也可用于www.example.cn、www.example2.com 等

**通配符SSL**

证书可以用于某个及其所有一级子域名
    
*.example.com的证书，也可用于www.example.com、cdn.example.com等

# 安装证书

CA厂商会提供证书的安装教程，所使用的Web服务器不同，安装的证书方式也不一样

以下是个人在安装DV SSL证书的一些做法，略作参考

## Linux + Nginx

1. 修改配置文件一般是通过修改全局配置文件实现，全局配置文件通常位于 `/ect/nginx/nginx.conf`
2. 如果服务器允许多个站点，推荐通过修改站点的配置来实现，站点的配置文件一般位于目录 `/etc/nginx/conf.d/`
3. 打开自定义的配置文件 `vi sever.conf`，在 `server` 节点，监听 `443` 端口

```
    server {
            listen 443 ssl;
            server_name example.com;
            ssl on;
            ssl_certificate cert/214181760910328.pem;
            ssl_certificate_key cert/214181760910328.key;
            ssl_session_timeout 5m;
            keepalive_timeout 90;
            ssl_prefer_server_ciphers on;
    }
```

把http的请求强制转到https

    server {
        listen 80;
        server_name example.com www.example.com;
        rewrite ^(.*) https://example.com$1 permanent;
    }

然后重启nginx服务

```
nginx -s reload
```

## eclipse + tomcat

1.打开服务器的 `server.xml` 文件

```
<Connector port="443" protocol="org.apache.coyote.http11.Http11NioProtocol"
    maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
    keystoreFile="C:\i-cert\214181760910328.pfx"
    keystoreType="PKCS12"
    keystorePass="214181760910328"
    clientAuth="false" sslProtocol="TLS" />
```

2.在服务器 `web.xml` 文件结尾添加

把http的请求强制转到https

```
<security-constraint>
    <web-resource-collection >
        <web-resource-name>SSL</web-resource-name>
        <url-pattern>/*</url-pattern>
    </web-resource-collection>                             
    <user-data-constraint>
        <transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
</security-constraint>
```

# 注意事项

## 升级静态资源

1. 想要全站点都是绿色小锁头，必须确保所有的站点资源（图片、js、css）都是https链接
2. 如果站点中存在非https的链接引用
    1. Chrome浏览器https变灰色
    2. Android5.0 API默认仅支持一种模式，http资源将不会被加载，需要自行设置WebSetting属性为`WebSettings.MIXED_CONTENT_ALWAYS_ALLOW`

## 提高安全措施

### HTTP Strict Transport Security (HSTS)

访问网站时，用户很少直接在地址栏输入`https://`，总是通过点击链接，或者301重定向，从HTTP页面进入HTTPS页面，攻击者完全可以在用户发出HTTP请求时，劫持并篡改该请求。

另一种情况是恶意网站使用自签名证书，冒充另一个网站，这时浏览器会给出警告，但是许多用户会忽略警告继续访问

"HTTP严格传输安全"（HSTS）的作用，就是强制浏览器只能发出HTTPS请求，并阻止用户接受不安全的证书
它在网站的响应头里面，加入一个强制性声明。

以下例子摘自[Wiki](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security)

```
Strict-Transport-Security: max-age=31536000; includeSubDomains
```

上面这段头信息有两个作用

1. 在接下来的一年（即31536000秒）中，浏览器只要向example.com或其子域名发送HTTP请求时，必须采用HTTPS来发起连接。用户点击超链接或在地址栏输入 `http://www.example.com`，浏览器应当自动将http转写成https，然后直接向 `https://www.example.com` 发送请求。
2. 在接下来的一年中，如果example.com服务器发送的证书无效，用户不能忽略浏览器警告，将无法继续访问该网站。

`HSTS` 很大程度上解决了`SSL` 剥离攻击

只要浏览器曾经与服务器建立过一次安全连接，即使链接被换成了HTTP，之后浏览器会强制使用HTTPS
该方法的主要不足是，用户首次访问网站发出HTTP请求时，是不受HSTS保护的

### Cookie

另一个需要注意的地方是，确保浏览器只在使用 HTTPS 时，才发送Cookie

网站响应头里面，Set-Cookie字段加上Secure标志即可。

```html
    Set-Cookie: value[; expires=date][; domain=domain][; path=path][; secure]
```

