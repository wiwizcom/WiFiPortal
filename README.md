# 拼拼WiFi / Wiwiz for OpenWrt

## 简介
拼拼WiFi / Wiwiz平台的OpenWrt固件插件。可以很方便的实现WiFi的网页认证、收费WiFi功能。

[完整的固件编译教程](https://mp.weixin.qq.com/s/ibuAdO1-wwolK-DIv81z9w)

已编译好的数百种设备的固件文件：http://www.wiwiz.com/pinpinwifi/firmware.htm

## 关于拼拼WiFi
拼拼WiFi是基于Wiwiz平台开发的专门用于实现收费WiFi的系统。
[拼拼WiFi介绍](http://www.wiwiz.com/pinpinwifi/#docs)

## 安装到OpenWrt
准备好OpenWrt的源码，假设源码目录名为OPENWRT_DIR。

获取本项目代码，将eqos-master-wiwiz与wifidog-wiwiz目录拷贝至OpenWrt源码目录的package目录下。操作如下：

```
git clone https://github.com/wiwizcom/WiFiPortal.git
#如访问不了github请使用gitee
#git clone https://github.com/wiwizcom/WiFiPortal.git

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

1. LuCI ---> Applications ---> luci-app-eqos

2. Network ---> Captive Portals ---> wifidog-wiwiz

以下项目也建议选择：

3. LuCI ---> Collections  ---> luci

4. LuCI ---> Modules ---> luci-compat


编译应用包
```
make package/eqos-master-wiwiz/compile V=s
make package/wifidog-wiwiz/compile V=s
```

如需编译整个固件，则执行：
```
make V=s
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

## 友情提醒
编译凭耐心，刷机需经验，操作有风险，变砖莫悲伤！

## 更新日志
2021-09-09：首次发布

2022-02-28：功能改进 - 重启后已认证用户可以无感免认证
