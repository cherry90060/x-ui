首先更新及安装组件

apt update -y          # Debian/Ubuntu 命令

apt install -y curl    #Debian/Ubuntu 命令

apt install -y socat    #Debian/Ubuntu 命令

yum update -y          #CentOS 命令

yum install -y curl    #CentOS 命令

yum install -y socat    #CentOS 命令

安装 Acme 脚本

curl https://get.acme.sh | sh

80 端口空闲的证书申请方式

自行更换代码中的域名、邮箱为你解析的域名及邮箱

~/.acme.sh/acme.sh --register-account -m xxxx@xxxx.com

~/.acme.sh/acme.sh  --issue -d mydomain.com   --standalone

安装证书到指定文件夹

自行更换代码中的域名为你解析的域名

~/.acme.sh/acme.sh --installcert -d mydomain.com --key-file /root/private.key --fullchain-file /root/cert.crt

安装证书

不安装证书也可以安装x-ui面板

安装 & 升级 X-ui 面板

安装及升级的一键代码

节点配置及功能讲解
# x-ui
支持多协议多用户的 xray 面板

# 功能介绍
- 系统状态监控
- 支持多用户多协议，网页可视化操作
- 支持的协议：vmess、vless、trojan、shadowsocks、dokodemo-door、socks、http
- 支持配置更多传输配置
- 流量统计，限制流量，限制到期时间
- 可自定义 xray 配置模板
- 支持 https 访问面板（自备域名 + ssl 证书）
- 更多高级配置项，详见面板

# 安装&升级
```
bash <(curl -Ls https://raw.githubusercontent.com/cherry90060/x-ui/master/install.sh)
```
## 手动安装&升级
1. 首先从 https://github.com/vaxilu/x-ui/releases 下载最新的压缩包，一般选择`amd64`架构
2. 然后将这个压缩包上传到服务器的`/root/`目录下，并使用`root`用户登录服务器

> 如果你的服务器 cpu 架构不是`amd64`，自行将命令中的`amd64`替换为其他架构

```
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-amd64.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

## 建议系统
- CentOS 7+
- Ubuntu 16+
- Debian 8+

# 常见问题

## 从 v2-ui 迁移
首先在安装了 v2-ui 的服务器上安装最新版 x-ui，然后使用以下命令进行迁移，将迁移本机 v2-ui 的`所有 inbound 账号数据`至 x-ui，`面板设置和用户名密码不会迁移`
> 迁移成功后请`关闭 v2-ui`并且`重启 x-ui`，否则 v2-ui 的 inbound 会与 x-ui 的 inbound 会产生`端口冲突`
```
x-ui v2-ui
```

## Stargazers over time

[![Stargazers over time](https://starchart.cc/vaxilu/x-ui.svg)](https://starchart.cc/vaxilu/x-ui)
