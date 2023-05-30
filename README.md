# IP地址配置

```shell
##主机伺服
system-view
## 选着网口 
interface GigabitEthernet 网口
## 配置ip
ip address ip 子网掩码
## 退出保存
quit
save
```

# 路由器开启DHCP
```shell
system-view
## 开启DHCP服务
dhcp enable
```

# dns域名系统

```shell
## 路由器设置
interface GigabitEthernet 网口
### 选择接口
dhcp select interface
dhcp server dns-list dns服务器地址
```

# 路由技术基础
+ 网关：用来连接不同网段的机器
```shell
## 添加路由表
ip route-static 跳转目标域 255.255.255.0 跳转网关ip
## 有去有回才能通
```
# TCP和UDP的区别
+ TCP：可靠性高，适合对文件传输的完整性要求高，但对延迟不敏感
  +  例如： 电子邮件
# VLAN虚拟局域网
+ 交换机的接口技术
   + Access：用来连接终端的
   + Trunk：用来连接其他交换机的
```shell
## 创建vlan
vlan vlan-id
## 查看创建vlan
display vlan
## 端口添加vlan
## 选择端口
int g端口
## 选择模式
port link-type 模式
## 将端口添加进vlan
port default vlan vlan-id
## trunk模式允许通过vlan
port trunk allow-pass vlan vlan-id/all
```
# 三层交换机
```shell 
# 选择vlan
int Vlanif vlan-id
```
# NAT
## 如何连接互联网
+ 路由器在怎么写
  + 写缺省路由 `ip route 0.0.0.0 0.0.0.0 下一跳
+ NAT网络地址转换
  + PC 手机在内网 用私网地址：192.168.x.x  10.x.x.x 172.16.x.x 到 172.31.x.x
  + 必须转换成公网地址
```shell
##创建NAT转换规则
## 1.创建acl规则
acl name acl-name neiwang basic
rule permit source 192.168.0.0 0.0.255.255
q
## 2.创建转换规则
nat address-group nat-id 64.1.1.2 64.1.1.6
## 3.规则连接
dis acl all ##查看acl编号
## 4.进入路由器出口设置
nat outbound acl-id address-group nat-id
## 5.固定nat地址
## 在服务器路由上配置回拨规则
ip route-static 10.1.1.0 255.255.255.0 119.1.1.2
int g 外出端口
nat server global 固定地址 inside 内网地址
```
# 远程管理设备telenet

```shell
## 创建远程连接用户数量 
user-interface vty x y
## 设置远程连接模式 aaa:user passworld    password:单密码
authentication-mode aaa
## 创建用户密码  cipher:密码加密
local-user testuser password cipher 123456
## 给用户权限 1-15数字越大权限越高
local-user testuser privilege level 15

```