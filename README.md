# 拼拼WiFi / Wiwiz for OpenWrt

## 关于拼拼WiFi
拼拼WiFi是基于Wiwiz平台开发的专门用于实现收费WiFi的系统。
[拼拼WiFi介绍](http://www.wiwiz.com/pinpinwifi/#docs)

## 安装到OpenWrt

准备好OpenWrt的源码，假设源码目录名为OPENWRT_DIR。
将eqos-master-wiwiz与wifidog-wiwiz目录拷贝至OpenWrt源码目录的package目录下。

```
cp -r eqos-master-wiwiz OPENWRT_DIR/package/
cp -r wifidog-wiwiz OPENWRT_DIR/package/

cd OPENWRT_DIR
./scripts/feeds update -a
./scripts/feeds install -a

make menuconfig
```

选择以下项目：
1. LuCI > Applications > luci-app-eqos
2. Network > Captive Portals > wifidog-wiwiz
	
```
make package/eqos/compile V=s
make package/wifidog-wiwiz/compile V=s
```

## 使用方法
1. 注册拼拼WiFi平台账户：
[拼拼WiFi平台注册/登录地址](http://www.wiwiz.com/pinpinwifi)
2. 创建一个场所，记下场所的Hotspot ID。
3. 进入OpenWrt的Web管理界面，进入Wiwiz菜单，填写Hotspot ID，勾选Enabled项，点击“保存并应用”。


## 功能限制与已知问题
暂不支持远程设备管理(DCC)功能；
不支持Wiwiz平台的插播广告（网页内植入悬浮广告）功能。

## Bug报告
EMail: support@wiwiz.com