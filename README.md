# 拼拼WiFi / Wiwiz for OpenWrt

## 简介
拼拼WiFi / Wiwiz平台的OpenWrt固件插件。可以很方便的实现WiFi的网页认证、收费WiFi与设备远程管理功能。

已编译好的数百种设备的固件文件：http://www.wiwiz.com/pinpinwifi/firmware.htm

[完整的编译步骤讲解](https://mp.weixin.qq.com/s/uT_BqWSt5mqIdh3stK7CwA)

## 关于拼拼WiFi
拼拼WiFi是基于Wiwiz平台开发的专门用于实现收费WiFi的系统。
[拼拼WiFi介绍](http://www.wiwiz.com/pinpinwifi/#docs)

## 安装到OpenWrt
准备好OpenWrt的源码，假设源码目录名为OPENWRT_DIR。

获取本项目代码，将dcc2-wiwiz、eqos-master-wiwiz与wifidog-wiwiz目录拷贝至OpenWrt源码目录的package目录下。操作如下：

```
git clone https://github.com/wiwizcom/WiFiPortal.git
#git clone https://gitee.com/wiwiz/WiFiPortal.git

cp -r dcc2-wiwiz OPENWRT_DIR/package/
cp -r eqos-master-wiwiz OPENWRT_DIR/package/
cp -r wifidog-wiwiz OPENWRT_DIR/package/

cd OPENWRT_DIR
./scripts/feeds update -a
./scripts/feeds install -a
```

配置OpenWrt应用包
```
make menuconfig
```

选择以下项目（必选）：

1. Wiwiz/PinPinWiFi  --->  Portal  ---> luci-app-eqos
2. Wiwiz/PinPinWiFi  --->  Portal  ---> wifidog-wiwiz
3. Wiwiz/PinPinWiFi  --->  Utilities  ---> dcc2-wiwiz-nossl
4. LuCI ---> Collections  ---> luci-ssl-openssl


以下项目也建议选择：

1. LuCI ---> Collections  ---> luci
2. LuCI ---> Modules ---> luci-compat


编译应用包
```
make package/eqos-master-wiwiz/compile V=s
make package/wifidog-wiwiz/compile V=s
make package/dcc2-wiwiz/compile V=s
make package/autokick-wiwiz/compile V=s
```

如需编译整个固件，则执行：
```
make V=s
```

## Web认证/收费功能的设置方法（绑定Hotspot ID）
1. 注册拼拼WiFi平台账户：
[拼拼WiFi平台注册/登录地址 http://www.wiwiz.com/pinpinwifi](http://www.wiwiz.com/pinpinwifi)
2. 创建一个场所，记下场所的Hotspot ID。
3. 进入OpenWrt的Web管理界面，进入 Wiwiz -> Portal 菜单，填写Hotspot ID，勾选“启用”项，点击“保存并应用”。

## 设备远程管理（DCC2）的设置方法
1. 登录DCC2后台，网址是：http://cp.wiwiz.com/ppwf/dcc2
2. 点击右上角账号，点击“显示Token”，并记下Token。
3. 进入OpenWrt的Web管理界面，进入 Wiwiz -> DCC2 菜单，填写用户Token，勾选“启用”项，点击“保存并应用”。

## 功能限制与已知问题
1. 暂不支持远程设备管理(DCC)功能（如需远程管控设备，请使用DCC2）；
2. 不支持Wiwiz平台的插播广告（网页内植入悬浮广告）功能；
3. 访问https网页加载认证页面时，浏览器会提示自签名安全证书警告。

## Bug报告
EMail: support@wiwiz.com

## 友情提醒
编译凭耐心，刷机需经验，操作有风险，变砖莫悲伤！

## 疑难问题
### 1. 手机或电脑连接后不显示认证页面，而是可以正常上网
确认外网的网线是否接的是WAN口（不可以是LAN口）。

确认是否绑定了Hotspot ID。

如果用的是OpenWrt 22.03及以后的版本编译的，那么make menuconfig之后检查这几项是否勾选了：
1. Network  --->  Firewall  --->  iptables-legacy
2. Network  --->  Firewall  --->  iptables-mod-conntrack-extra
3. Network  --->  Firewall  --->  iptables-mod-iface
4. Network  --->  Firewall  --->  iptables-mod-ipmark
6. Network  --->  Firewall  --->  ip6tables-legacy

## 更新日志
2021-09-09：首次发布

2022-02-28：功能改进 - 重启后已认证用户可以无感免认证

2022-04-10: 增加设备远程管理功能（DCC2）；一些功能优化

2022-05-08: 增加了https跳转功能

2022-07-06: 修复已知问题

2022-08-16: 修复已知问题，提高稳定性

2022-08-28: 修复已知问题，提高稳定性

2022-08-31: Bug修复；增加调试日志输出能力

2022-09-09: Bug修复

2022-10-09: 修复已知问题

2022-10-14: 修复部分设备DCC2设置后不能实时生效的问题

2022-10-21: 认证漫游优化

2022-10-23: 修复已知问题

2022-10-25: 新增免认证网络配置

2022-10-27: 进行了一些优化：绑定时省略用户名，显示版本号等

2022-10-30: 解决多WAN冲突问题

2022-12-10: 过滤Hotspot ID前后的空格

2023-08-15: 设置页面内增加了使用说明

2023-11-10: 适配OpenWrt 23.05；修复“multiple definition of XXX...”的问题

2024-01-09: 修复防火墙规则清空后Portal失效的问题

2024-06-13: 增加Portal认证到期后自动断开无线用户功能（autokick-wiwiz）

2024-06-22: Portal可指定网络接口；增加NoPortal功能支持
