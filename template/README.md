### 基本的模板
<details><summary>点击以查看模板</summary>

````
# 配置中的 # 符号是注释符号，你可以任意修改/删除有 # 符号的那一行
# The # symbol in the configuration is a comment symbol,
# You can arbitrarily modify/delete the line with the # sign.

port: 7890
socks-port: 7891
allow-lan: false
mode: Rule
log-level: info
external-controller: 127.0.0.1:9090

# 节点信息
proxies:
- name: "ss1"
  type: ss
  server: server
  port: 443
  cipher: chacha20-ietf-poly1305
  password: "password"
  # udp: true  

- name: "ss2"
  type: ss
  server: server
  port: 443
  cipher: AEAD_CHACHA20_POLY1305
  password: "password"
  plugin: obfs
  plugin-opts:
    mode: tls
    host: bing.com
# 节点群组
proxy-groups:
- name: "Proxy"
  type: select
  proxies:
  - "ss1"
  - "ss2"
- name: "Google"
  type: select
  proxies:
  - "ss1"
  - "ss2"
# 规则
rules:
# Google
- DOMAIN-SUFFIX,google.com,Google
- DOMAIN-KEYWORD,google,Google

# Proxy
- MATCH,Proxy
````
</details>