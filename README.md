## 🤔 这是什么？
- 它是一个网上工具。

## 🚀 快速上手

### 1. 安装`Docker`和`Docker compose`

- `Docker`安装教程：[https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)
- `Docker compose`安装教程：[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)
- `个人普通电脑`安装教程：https://docs.docker.com/get-docker/
- `docker镜像主页` https://docker.fxxk.dedyn.io/r/duqn/openwrt

### 2. 下载image

```bash
docker pull duqn/openwrt
```

### 3. 容器配置

- Linux 容器配置
```
ip link set eth0 promisc on
docker network create -d macvlan –subnet=10.10.10.0/24 –gateway=10.10.10.1 -o parent=eth0 openwrt
docker run –restart always –name openwrt -d –network openwrt 
```
- RouterOS容器配置
  
nano /etc/config/firewall
```
config interface 'lan'
	option device 'eth0'
	option proto 'static'
	option ipaddr '<IP under the local bridge>'
	option gateway '<RouterOS local bridge IP>'
	option dns '8.8.8.8'
	list ip6addr '<IPv6 under the local bridge>'
	list ip6gw '<RouterOS local bridge IPv6>'
```
`/etc/init.d/network restart`
```
SYN-flood disabled
```
`/etc/init.d/firewall restart`


### 4.离线部署
下载好的duqn_openwrt-amd64.tar文件上传到docker目录下（示例将文件上传至mnt/nvme0n1-4/duqn_openwrt-amd64.tar）

```
cd /mnt/nvme0n1-4/
```
```  
ls
```
```
docker load -i duqn_openwrt-amd64.tar
```

等待一会，此时镜像文就导入到docker中了，接下来使用docker run来执行镜像。
```
docker run -d \
  --restart unless-stopped \
  --name openwrt \
  -v "/tmp/upload:/openwrt/shells/data" \
  -e PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/lib/android-sdk/platform-tools \
  duqn/openwrt:latest
```
注意此命令中的端口为示例
```
 -v "/tmp/upload:/openwrt/shells/data" \
# 这目录是用来存放apk的，对应脚本里的批量安装apk的功能。如果你要使用该功能，你就关注一下映射的目录。
# 若不需要修改，则默认用/tmp/upload 目录来存放apk，你可以将需要安装的apk复制到该目录下即可。
```


## 在哪里可以搜索或查询docker镜像的详细信息
### [查询镜像的详细信息 点击这里直达](https://docker.fxxk.dedyn.io/)



