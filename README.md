# 拼拼WiFi / Wiwiz for OpenWrt

## 简介
拼拼WiFi / Wiwiz平台的OpenWrt固件插件。可以很方便的实现WiFi的网页认证、收费WiFi与设备远程管理功能。

已编译好的数百种设备的固件文件：http://www.wiwiz.com/pinpinwifi/firmware.htm

## 关于拼拼WiFi
拼拼WiFi是基于Wiwiz平台开发的专门用于实现收费WiFi的系统。
[拼拼WiFi介绍](http://www.wiwiz.com/pinpinwifi/#docs)

## 安装到OpenWrt
准备好OpenWrt的源码，假设源码目录名为OPENWRT_DIR。

获取本项目代码，将dcc2-wiwiz、eqos-master-wiwiz与wifidog-wiwiz目录拷贝至OpenWrt源码目录的package目录下。操作如下：

```
git clone https://github.com/wiwizcom/WiFiPortal.git
#如访问不了github请使用gitee
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


以下项目也建议选择：

3. LuCI ---> Collections  ---> luci

4. LuCI ---> Modules ---> luci-compat


编译应用包
```
make package/eqos-master-wiwiz/compile V=s
make package/wifidog-wiwiz/compile V=s
make package/dcc2-wiwiz/compile V=s
```

如需编译整个固件，则执行：
```
make V=s
```

## Web认证/收费功能的设置方法
1. 注册拼拼WiFi平台账户：
[拼拼WiFi平台注册/登录地址 http://www.wiwiz.com/pinpinwifi](http://www.wiwiz.com/pinpinwifi)
2. 创建一个场所，记下场所的Hotspot ID。
3. 进入OpenWrt的Web管理界面，进入 Wiwiz -> Portal 菜单，填写Hotspot ID，勾选“启用”项，点击“保存并应用”。

## 设备远程管理（DCC2）的设置方法
1. 登录DCC2后台，网址是：http://cp.wiwiz.com/ppwf/dcc2
2. 点击右上角账号，点击“显示Token”，并记下Token。
3. 进入OpenWrt的Web管理界面，进入 Wiwiz -> DCC2 菜单，填写用户TOken，勾选“启用”项，点击“保存并应用”。

## 功能限制与已知问题
暂不支持远程设备管理(DCC)功能（如需远程管控设备，请使用DCC2）；

不支持Wiwiz平台的插播广告（网页内植入悬浮广告）功能。

## Bug报告
EMail: support@wiwiz.com

## 友情提醒
编译凭耐心，刷机需经验，操作有风险，变砖莫悲伤！

## 更新日志
2021-09-09：首次发布

2022-02-28：功能改进 - 重启后已认证用户可以无感免认证

2022-04-10: 增加设备远程管理功能（DCC2）；一些功能优化
