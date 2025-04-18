---
hide:
  - toc
---

# 基础配置

smartdns配置的选项，功能比较丰富，但作为最基本的DNS服务，只需要配置服务端口号和上游服务器即可，其他参数默认情况下，对于家庭本地网络已经是最佳配置，无需做过多的修改。

## 配置样例

1. 在smartdns.conf配置文件中，包含配置如下即可提供服务并对DNS查询加速：

    ```shell
    # 监听53端口
    bind [::]:53
    # 配置上游服务器
    server 8.8.8.8
    server 114.114.114.114
    server 202.96.128.166:53
    server-tls 1.1.1.1
    server-quic 1.1.1.1
    server-h3 223.5.5.5
    ```

    选项中:

    * bind表示开启服务端，并监听对应的端口，`:53`表示绑定IPV4的53端口，`[::]:53`表示绑定IPV6的53端口，后者在大部分系统中，同时也绑定了IPV4端口。
    * server表示上游服务器IP地址，端口可以省略。如需要安全访问上游，可以使用server-tls, server-https, server-quic, server-h3。也可以使用URI方式，如server tls://1.1.1.1:853
    * server不指定的情况下，将会自动读取`/etc/resolv.conf`文件中的系统DNS地址。
