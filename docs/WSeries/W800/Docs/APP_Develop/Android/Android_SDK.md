<center><font size=10> W800_BleWiFi Bluetooth Connection Android SDK </center></font>
<center> From SZDOIT</center>

## 1 The Introduction

### 1.1 Overview

BleWiFi is a low power Bluetooth (BLE) channel based protocol for WiFi network configuration, suitable for W800 chip.

This document introduces the use method of BleWiFi for Android SDK interface provided by our company, so as to facilitate the secondary development of BleWiFi and quickly integrate BleWiFi into our Own Android App.

## 2 The Interface Definition

### 2.1 BleWiFiClient Class

This class provides all the apis for communicating with Device, which makes it easy for an APP to configure a Device via Bluetooth BLE.

#### 2.1.1 The Constructor

This constructor returns an instance of the BleWiFiClient class.

Prototype:

public BleWiFiClient(Context context, BluetoothDevice device);

Parameters:

context：Apply Context;

device：Equipment to be configured;

#### 2.1.2 The Connect Method

This method establishes the connection between client and Device. If the connection is established successfully, the BleWiFiCallback callback onConnected method will be called. The BleWiFiCallback callback onServicesDiscovered method is invoked after the client actively scans the Device's services and characteristics. The user can then begin the networking process after discovering the specified services and characteristics.

Prototype:

public synchronized void connect() ;

#### 2.1.3 negotiateSecretKey methods

This method used to Device holds's secret cipher key, holds bear fruit through BleWiFiCallback callback method onNegotiateSecretKeyResult notification to the user.

Prototype:

public void negotiateSecretKey();

#### 2.1.4 configureSta Methods

This method configures Device as the parameter of STA. After successful configuration, Device will be netted, and the netted result will be notified to the user through the BleWiFiCallback callback to onConfigureStaResult method.

Prototype:

public void configureSta(final BleWiFiStaParams params);

Parameter：

params：Configure STA parameters, including SSID and PASSWORD of AP;

#### 2.1.5 setBleWiFiCallback Methods

本方法用来设置 client 的 BleWiFiCallback 回调接口。

Prototype：

public void setBleWiFiCallback(BleWiFiCallback callback);

Parameter：

callback：BleWiFiCallback callback interface instance;

#### 2.1.6 close methods

This method is used to free the client's resources.

Prototype:

public synchronized void close();

### 2.2 Callback Interface

This interface is used to implement callbacks to the BleWiFiClient class. The user's callback class needs to inherit this interface and set an instance of the callback class to the client via the BleWiFiClient setBleWiFiCallback method to receive notifications.

#### 2.2.1 onConnected Methods

This method is used to notify the user that the Bluetooth connection has been established successfully.

Prototype：

void onConnected(BleWiFiClient client);

Parameter：

client：An instance of BleWiFiClient class;

#### 2.2.2 onDisconnected Methods

This method is used to notify the user that the Bluetooth connection has been disconnected.

Prototype：

void onDisconnected(BleWiFiClient client);

Parameter：

client：An instance of BleWiFiClient class;

#### 2.2.3 onServicesDiscovered Methods

This method is used to inform the user that the Bluetooth GATT services and features have been discovered and the user can start the key exchange process in this callback method. If you do not need to encrypt the transport configuration parameters, you can skip the key exchange process and start the networking process directly in this callback method.

Prototype：

void onServicesDiscovered(BleWiFiClient client);

Parameter：

client：An instance of BleWiFiClient class;

#### 2.2.4 onConfigureStaResult Methods

This method is used to notify the user of the configuration result of the call to client.configuresta method.

Prototype：

void onConfigureStaResult(BleWiFiClient client, BleWiFiConfigStaResult result);

Parameter：

client：An instance of BleWiFiClient class;

result：Distribution network results;

#### 2.2.5 onNegotiateSecretKeyResult Methods

This method is used to inform the user invokes the client negotiateSecretKey method of key exchange.

Prototype：

void onNegotiateSecretKeyResult(BleWiFiClient client, BleWiFiBaseResult

result);

Parameter：

client：An instance of BleWiFiClient class;

result：Key exchange results;

#### 2.2.6 onError Methods

This method is used to notify the user of an error.

Prototype：

void onError(BleWiFiClient client, int errCode);

Parameter：

client：An instance of BleWiFiClient class;

errCode：Error number;

### 2.3 BleWiFiStaParams Class

This class is the parameter class for the configureSta configuration method of the BleWiFiClient class, containing SSID, Password, and

The three BSSID parameters can be set, with at least one of the SSID and BSSID not set to null. If AP is an OPEN module

Where, password is not set.

#### 2.3.1 setSsid Methods

本方法用来设置 AP 的 SSID。

原型：

public void setSsid(String ssid);

参数：

ssid：AP 的 SSID；

#### 2.3.2 setPassword 方法

本方法用来设置 AP 的密码。

原型：

public void setPassword(String password);

参数：

password：AP 的密码；

#### 2.3.3 setBssid 方法

本方法用来设置 AP 的 BSSID，本方法适用于隐藏 SSID 的 AP 配网的情况，可以通过设

置 BSSID 和 Password 来配网。

原型：

public void setBssid(String bssid);

参数：

bssid：AP 的 BSSID；

### 2.4 BleWiFiBaseResult 类

本类是 BleWiFiCallback 回调接口 onNegotiateSecretKeyResult 方法的参数类。也是

所有回调接口方法参数类的基类。

#### 2.4.1 getStatus 方法

本方法用来获取回调接口方法的状态，通知用户结果。

原型：

public int getStatus();

返回值：

错误号，具体参见本类错误号定义。

#### 2.4.2 错误号定义

本类定义了如下错误号，包含了 getStatus 方法返回的所有可能值，同时也包含了

BleWiFiCallback 回调接口 onError 方法所有的错误。

//成功

public static final int STATUS_SUCCESS = 0;

//参数错误

public static final int STATUS_INVALID_PARAMS = 1;

//密码错误

public static final int STATUS_PASSWORD = 2;

//获取 IP 地址失败



public static final int STATUS_DHCP_IP= 3;

//扫描失败

public static final int STATUS_WIFI_SCAN= 4;

//秘钥交换失败

public static final int STATUS_NEGOTIATE_SECRET_KEY=5;

//发送数据失败

public static final int STATUS_GATT_WRITE=6;

### 2.5 BleWiFiConfigStaResult 类

本类是 BleWiFiCallback 回调接口 onConfigureStaResult 方法的参数类。本类继承

BleWiFiBaseResult 类，除了 status 外，还有 mac 和 IPAddress 可以获取。

#### 2.5.1 getMac 方法

本方法用来获取 Device 的 WiFi Mac 地址，配网后加网成功后返回。

原型：

public String getMac();

返回值：

Device 的 WiFi Mac 地址。

#### 2.5.2 getIpAddress 方法

本方法用来获取 Device 的 IP 地址，配网后加网成功后返回。

原型：

public String getIpAddress();

返回值：

Device 的 IP 地址。

## 3 使用示例

### 3.1 实例化 BleWiFiClient

mBleWiFiClient = new BleWiFiClient(getApplicationContext(), mDevice);

### 3.2 设置 BleWiFiCallback

mBleWiFiClient.setBleWiFiCallback(new MyBleWifiCallback());

### 3.3 连接 Device

```
mBleWiFiClient.connect();

//连接成功在 BleWiFiCallback 回调接口中通知

@Override

public void onConnected(BleWiFiClient client) {

}

    //发现服务和特征在 BleWiFiCallback 回调接口中通知

    @Override

    public void onServicesDiscovered(BleWiFiClient client) {

    //发现服务和特征成功

    onGattServicesDiscovered();

}
```



### 3.4 与 Device 协商数据加密密钥

```
//发现服务和特征成功，开始密钥协商

private void onGattServicesDiscovered() {

//开始与 Device 协商数据加密密钥

mBleWiFiClient.negotiateSecretKey();

}

//协商结果在 BleWiFiCallback 回调接口中通知

@Override

public void onNegotiateSecretKeyResult(BleWiFiClient client,

BleWiFiBaseResult result) {

    if(result.getStatus() == BleWiFiBaseResult.STATUS_SUCCESS){

    //协商成功

        onNegotiateSecretKeySuccess();

    }

    else{

    }

}
```



### 3.5 开始配网

```
//协商成功，开始加密传输配网参数

private void onNegotiateSecretKeySuccess(){

runOnUiThread(() -> {

	//构造 STA 配网参数

    BleWiFiStaParams params = new BleWiFiStaParams();

    params.setSsid(mTxtSsid.getText().toString());

    params.setPassword(mTxtPassword.getText().toString());

    //开始配网



    mBleWiFiClient.configureSta(params);

    });

}

//配网结果在 BleWiFiCallback 回调接口中通知

@Override

public void onConfigureStaResult(BleWiFiClient client, BleWiFiConfigStaResult

result) {

    if(result.getStatus() == BleWiFiBaseResult.STATUS_SUCCESS) {

        //配网成功，显示 WiFi 的 Mac 地址和 Device 的 IP 地址

        ShowMessage(String.format("Mac: %s", result.getMac()));

        ShowMessage(String.format("IP Address: %s",

        result.getIpAddress()));

    }

    else{

    }

}
```





# 支持与服务

| 四博智联资源                                        |                                                              |
| --------------------------------------------------- | ------------------------------------------------------------ |
| 官网                                                | [www.doit.am](http://www.doit.am/)                           |
| 教材                                                | [ESPDuino智慧物联开发宝典](https://item.taobao.com/item.htm?spm=a1z10.3-c.w4002-7420449993.9.Bgp1Ll&id=520583000610) |
| 购买                                                | [官方淘宝店](https://szdoit.taobao.com/)(szdoit.am)          |
| 讨论                                                | [技术论坛](http://bbs.doit.am/forum.php)(bbs.doit.am)        |
| 应用案例集锦                                        |                                                              |
| [Doit玩家云](http://wechat.doit.am)(wechat.doit.am) | [免费TCP公网调试服务](http://tcp.doit.am)(tcp.doit.am)       |
| 官方技术支持QQ群1/2/3群已满                         |                                                              |
| 技术支持群4                                         | 278888904                                                    |
| 技术支持群5                                         | 278888905                                                    |
| 术支持群6                                           | 278888906                                                    |
| 技术支持群7                                         | 278888907                                                    |
| 技术支持群8                                         | 278888908                                                    |
| 技术支持群9                                         | 278888909                                                    |
| 技术支持群10                                        | 278888900                                                    |