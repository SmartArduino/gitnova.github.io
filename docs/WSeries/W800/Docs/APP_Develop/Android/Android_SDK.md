<center><font size=10> W800 BleWiFi Bluetooth Connection Android SDK </center></font>
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

Prototype：

public void setSsid(String ssid);

Parameter：

ssid：AP 的 SSID；

#### 2.3.2 setPassword Methods

This method is used to set the AP password.

Prototype：

public void setPassword(String password);

Parameter：

password：The AP password;

#### 2.3.3 setBssid Methods

This method is used to set the BSSID of AP. This method is suitable for AP network with SSID hidden

Set BSSID and Password to configure the network.

Prototype：

public void setBssid(String bssid);

Parameter：

bssid：AP 的 BSSID；

### 2.4 BleWiFiBaseResult Class

This class is BleWiFiCallback callback interface onNegotiateSecretKeyResult method the parameters of the class. Is also

Base class for all callback interface method parameter classes.

#### 2.4.1 getStatus Methods

This method is used to get the status of the callback interface method and notify the user of the result.

Prototype:

public int getStatus();

The return value：

Error number, see this class error number definition.

#### 2.4.2 Error number definition

This class defines the following error number, which contains all possible values returned by the getStatus method, and also contains

The BleWiFiCallback callback interface onError method has all the errors.

//succes

public static final int STATUS_SUCCESS = 0;

//Parameter error

public static final int STATUS_INVALID_PARAMS = 1;

//Password mistake

public static final int STATUS_PASSWORD = 2;

//Failed to get IP address

public static final int STATUS_DHCP_IP= 3;

//Scan fail

public static final int STATUS_WIFI_SCAN= 4;

//The secret key exchange failed

public static final int STATUS_NEGOTIATE_SECRET_KEY=5;

//Failed to send data

public static final int STATUS_GATT_WRITE=6;

### 2.5 BleWiFiConfigStaResult Cladd

This class is the parameter class for the BleWiFiCallback callback interface onConfigureStaResult method. This class inheritance

The BleWiFiBaseResult class, in addition to status, is also available for MAC and IPAddress.

#### 2.5.1 getMac Methods

This method is used to obtain the WiFi Mac address of the Device. After network configuration, it returns after successful network addition.

Prototype：

public String getMac();

The return value：

Device 的 WiFi Mac Address.

#### 2.5.2 getIpAddress Methods

This method is used to obtain the IP address of Device, and returns after the network is installed successfully.

Pritityoe：

public String getIpAddress();

The return value：

Device 的 IP Address.

## 3 Use the sample

### 3.1 Instantiation BleWiFiClient

mBleWiFiClient = new BleWiFiClient(getApplicationContext(), mDevice);

### 3.2 Set the BleWiFiCallback

mBleWiFiClient.setBleWiFiCallback(new MyBleWifiCallback());

### 3.3 Connect the Device

```
mBleWiFiClient.connect();

//A successful connection is notified in the BleWiFiCallback callback interface

@Override

public void onConnected(BleWiFiClient client) {

}

    //Discovery services and features are notified in the BleWiFiCallback callback interface

    @Override

    public void onServicesDiscovered(BleWiFiClient client) {

    //Discover successful services and features

    onGattServicesDiscovered();

}
```



### 3.4 Negotiate the data encryption key with Device

```
//Discover that the service and feature are successful, and begin key negotiation

private void onGattServicesDiscovered() {

//Begin negotiating the data encryption key with Device

mBleWiFiClient.negotiateSecretKey();

}

//The negotiation results are notified in the BleWiFiCallback callback interface

@Override

public void onNegotiateSecretKeyResult(BleWiFiClient client,

BleWiFiBaseResult result) {

    if(result.getStatus() == BleWiFiBaseResult.STATUS_SUCCESS){

    //Successful negotiation

        onNegotiateSecretKeySuccess();

    }

    else{

    }

}
```



### 3.5 Began to distribution network

```
//The negotiation is successful and encryption of transmission network parameters is started

private void onNegotiateSecretKeySuccess(){

runOnUiThread(() -> {

	//The parameters of STA distribution network are constructed

    BleWiFiStaParams params = new BleWiFiStaParams();

    params.setSsid(mTxtSsid.getText().toString());

    params.setPassword(mTxtPassword.getText().toString());

    //Began to distribution network

    mBleWiFiClient.configureSta(params);

    });

}

//The configuration results are notified in the BleWiFiCallback callback interface

@Override

public void onConfigureStaResult(BleWiFiClient client, BleWiFiConfigStaResult

result) {

    if(result.getStatus() == BleWiFiBaseResult.STATUS_SUCCESS) {

        //WiFi: Mac address and Device IP address are displayed

        ShowMessage(String.format("Mac: %s", result.getMac()));

        ShowMessage(String.format("IP Address: %s",

        result.getIpAddress()));

    }

    else{

    }

}
```

## Contact Us

- E-mails: [yichone@doit.am](mailto:yichone@doit.am), [yichoneyi@163.com](mailto:yichoneyi@163.com)
- Skype: yichone
- WhatsApp:+86-18676662425
- Wechat: 18676662425

