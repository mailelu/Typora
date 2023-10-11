# Web Servers

本lab主要是为了研究web service

前置:下载netstat(net-tools)

```shell
systemctl --type=<service name>
//查看service
systemctl stauts <service name>
//查看具体服务的状态

```



___

# DNS

下载bind9(域名解析服务器)并关闭dnsmasq

```shell
sudo apt purge dnsmasq  //卸载
systemctl stop bind9	//关闭bind9

systemctl cat bind9  	//查看服务内容
```

我们会发现一些熟悉的部分,这部分我们再Lab4见过



当你尝试使用两个不同又相似的命令

* `dig ocf.berkeley.edu @localhost`
* `dig ocf.berkeley.edu`



会得到截然不同的结果

为什么?Gpt的解释

1. `dig ocf.berkeley.edu @localhost`：这个命令将 `dig` 命令、要查询的主机名 `ocf.berkeley.edu` 和 DNS 服务器 `localhost` 分开。这意味着 `dig` 将查询 `ocf.berkeley.edu` 这个主机名，但它会将查询发送到本地的 DNS 服务器 `localhost` 来获取该主机名的 IP 地址。这是标准的 `dig` 查询方式，将查询发送到指定的 DNS 服务器以获取域名解析信息。
2. `dig ocf.berkeley.edu` 是一个用于进行 DNS（域名系统）查询的命令。它用来查找有关域名或主机名的信息，特别是用于查询域名 "ocf.berkeley.edu" 的 DNS 信息。



____

现在,我们正式开始DNS本地服务器的配置

##设置本地DNS的配置

```shell
vim /etc/bind/named.conf.local 
//打开本地配置
加入以下内容
zone "example.com" {
  type master;
  file "/etc/bind/db.example.com";
};
```

详细描述一下这个操作

1. 打开本地配置时,内容为空,原因是默认是没有本地配置的,要你自己去配置
2. 加入的内容大概意思就是:加入eample.com的域名以及解析的文件: **/etc/bind/db.example.com**
3. `type master;`：这一行指定了这个DNS区域的类型。在这里，它被设置为"master"，表示这个DNS服务器是该区域的主要控制者，即它负责维护和管理该区域的DNS记录。

## 配置db.example.com文件



配置文件最好的方式是先**找个模板**

```shell
;
; BIND data file example.com
;
$TTL	604800
@	IN	SOA	ns.example.com. root.example.com. (
				1		      
				; Serial
				604800		
				; Refresh
				86400		  
				; Retry
				2419200		
				; Expire
				604800 )	
				; Negative Cache TTL
;
        IN	NS	ns.example.com.

ns  IN  A   127.0.0.1                
; IP for name server (random ip)
@	IN	A	1.2.3.4                  
; A record for example.com (random ip)
; Add more records (Ex. CNAME, AAAA, MX, subdomains...)
```

* `;`表示注释
* `$TTL`表示DNS记录的生存时间
* `@`：这是一个特殊符号，表示当前域名，也就是"example.com"。
* `IN`：表示Internet类型的记录。
* `SOA`：SOA（Start of Authority）记录定义了区域的权威性和基本参数，包括域名服务器（ns.example.com）和相关的配置信息。
  - `ns.example.com.`：这是主名服务器的名称。
  - `root.example.com.`：这是管理者的电子邮件地址，应该替换为实际的电子邮件地址。
  - `1`：这是序列号，通常用于跟踪区域文件的更改。当您更新DNS记录时，应递增该值。
  - `604800`：刷新时间，表示其他DNS服务器多久需要重新获取区域文件的副本。
  - `86400`：重试时间，表示其他DNS服务器多久需要等待在刷新时间后进行重试。
  - `2419200`：过期时间，表示其他DNS服务器多久后不再信任此区域文件。
  - `604800`：负缓存TTL，表示其他DNS服务器对无效记录的缓存时间。
* `IN NS ns.example.com.`：这是一个Name Server（NS）记录，指定了名为"ns.example.com"的域名服务器。
* `ns IN A 127.0.0.1`：这是一个A记录，将"ns"映射到IP地址"127.0.0.1"，通常用于指定域名服务器的IP地址。
* `@ IN A 1.2.3.4`：这是另一个A记录，将"example.com"映射到IP地址"1.2.3.4"，这通常是您的网站的主机IP地址。



在末尾配置:

```shell
test IN A 93.184.216.34
```

重启服务

```shell
systemctl reload bind9	//使配置生效
```

这时候,我们用本地DNS查看一下example.com以及test.example.com

```shell
dig @localhost example.com
//显示1.2.3.4
dig @localhost test.example.com
//显示93.184.216.34
```



Q1:什么命令可以查看bind9

`systemctl status bind9`

Q2:为什么加了@localhost就会报错

因为本地DNS没有进行配置



# Load Balacing(负载均衡)

前言:本实验将用HAProxy来做负载均衡

* 对GNGINX来说,它最开始就是用来做负载均衡服务器的,但是HAPorxy同样也可以完成目的





