<center><font size=10> W800  BleWiFi Bluetooth Config Network  iOS SDK </center></font>
<center> From SZDOIT</center>

## 1 The Introduction

### 1.1 Overview

BleWiFi is a low power Bluetooth (BLE) channel based protocol for WiFi network configuration, suitable for W800 chip.

This document introduces the use method of BleWiFi for IOS SDK interface provided by our company, which is convenient for users to carry out the secondary development of BleWiFi and quickly integrate BleWiFi into their IOS App.

## 2 The Interface Definition

### 2.1 BleWiFiClient Cladd

This class provides all the apis for communicating with Device, which makes it easy for an APP to configure a Device via Bluetooth BLE.

#### 2.1.1 Initialization Function

This initialization function returns an instance of the BleWiFiClient class.

Prototype：

- (instancetype)initWithDevice:(CBPeripheral) device;

Parameter：

device：Equipment to be configured;

#### 2.1.2 connect Methods

This method establishes a connection between client and Device. If the connection is established successfully, the BleWiFiDelegate callback onConnected method will be called. The BleWiFiDelegate callback onServicesDiscovered method is invoked after the client actively scans the Device's services and features, and the user can begin the networking process after discovering the specified services and features.

Prototype：

- (void) connect;

#### 2.1.3 negotiateSecretKey methods

This method used to Device holds's secret cipher key, holds bear fruit through BleWiFiDelegate callback method onNegotiateSecretKeyResult notification to the user.

prototype：

- (void) negotiateSecretKey;

#### 2.1.4 configureSta methods

In this method, Device is configured as the parameter of STA. After successful configuration, Device will be netted, and the netted result will be notified to the user through the BleWiFiDelegate callback onConfigureStaResult method.

Prototype：

- (void) configureSta:(BleWiFiStaParams )params;

Parameter：

params：Configure STA parameters, including SSID and PASSWORD of AP;

#### 2.1.5 delegate attribute

This property is used to set up the Client's BleWiFiDelegate agent.

Prototyoe：

@property (nonatomic, weak)id<BleWiFiDelegate> delegate;

#### 2.1.6 close methods

This method is used to free the client's resources.

Prototype：

- (void) close;



### 2.2 BleWiFiDelegate The Agent

This agent is used to implement a callback to the BleWiFiClient class. The user receives notifications by setting the BleWiFiClient's delegate property and implementing the proxy's method.

#### 2.2.1 onConnected methods

This method is used to notify the user that the Bluetooth connection has been established successfully.

Prototype：

- (void)onConnected:(BleWiFiClient )client;

Parameter：

client：An instance of BleWiFiClient class;

#### 2.2.2 onDisconnected methods

This method is used to notify the user that the Bluetooth connection has been disconnected.

Prototype：

- (void)onDisconnected:(BleWiFiClient )client;

Parameter：

client：An instance of BleWiFiClient class;

#### 2.2.3 onServicesDiscovered methods

This method is used to inform the user that the Bluetooth GATT services and features have been discovered and the user can start the key exchange process in this callback method. If you do not need to encrypt the transport configuration parameters, you can skip the key exchange process and start the networking process directly in this callback method.

Prototype：

- (void)onServicesDiscovered:(BleWiFiClient )client;

Parameter：

client：An instance of BleWiFiClient class;

#### 2.2.4 onConfigureStaResult methods

This method is used to notify the user of the configuration result of the call to client.configuresta method.

Prototype：

- (void)onConfigureStaResult:(BleWiFiClient )client

Result:(BleWiFiConfigStaResult )result;

Parameter：

client：An instance of BleWiFiClient class;

result：Distribution network results;

#### 2.2.5 onNegotiateSecretKeyResult methods

This method is used to inform the user invokes the client negotiateSecretKey method of key exchange.

Prototype：

- (void)onNegotiateSecretKeyResult:(BleWiFiClient )client

Result:(BleWiFiBaseResult )result;

Parameter：

client：An instance of BleWiFiClient class;

result：Key exchange results;

#### 2.2.6 onError methods

This method is used to notify the user of an error.

Prototype：

- (void)onError:(BleWiFiClient )client Error:(int)errCode;

Parameter：

client：An instance of BleWiFiClient class;

errCode：Error number;

### 2.3 BleWiFiStaParams Class

This class is the parameter class of configureSta configuration method of BleWiFiClient class. It contains three parameters: SSID, Password and BSSID, which can be set. At least one of the SSID and BSSID can be set without null. If AP is OPEN mode, password is not set.

#### 2.3.1 ssid attribute

This property sets the SSID for the AP.

Prototype:

@property (strong, nonatomic) NSString ssid;

#### 2.3.2 Password attributes

This property is used to set the password for the AP.

Prototype：

@property (strong, nonatomic) NSString password;

#### 2.3.3 bssid attributes

This property is used to set the BSSID of AP. This property is suitable for AP network configuration with SSID hidden. BSSID and Password can be set to configure the network.

Prototype：

@property (strong, nonatomic) NSString bssid;

## 2.4 BleWiFiBaseResult Class

This class is BleWiFiDelegate agent onNegotiateSecretKeyResult method the parameters of the class. It is also the base class for all the callback method parameter classes of the BleWiFiDelegate agent.

#### 2.4.1 status attributes

This property is used to get the state of the callback interface method and notify the user of the result, as defined in the error number in the class header file.

Prototype：

@property (assign, nonatomic) int status;

#### 2.4.2 Error number definition

This class header file defines the following error number, which contains all possible values for the status attribute, as well as all errors for the BleWiFiDelegate agent onError method.

```
//success

#define STATUS_SUCCESS 0

//Parameter error

#define STATUS_INVALID_PARAMS 1

//Password mistake

#define STATUS_PASSWORD 2

//Failed to get IP address

#define STATUS_DHCP_IP 3

//Scan fail

#define STATUS_WIFI_SCAN 4

//The secret key exchange failed

#define STATUS_NEGOTIATE_SECRET_KEY 5

//Failed to send data

#define STATUS_GATT_WRITE 6
```

### 2.5 BleWiFiConfigStaResult Class

This class is the parameter class for the BleWiFiDelegate agent onConfigureStaResult method. This class inherits the BleWiFiBaseResult class, which is available in addition to status, MAC and IPAddress.

#### 2.5.1 mac attributes

This property is used to obtain the WiFi Mac address of the Device. After network configuration, the Device will be returned after successful network addition.

Prototype：

@property (strong, nonatomic) NSString mac;

#### 2.5.2 ipAddress attributes

This property is used to obtain the IP address of Device, and returns after the Device is installed on the network.

Prototype：

@property (strong, nonatomic) NSString ipAddress;

## 3 Use the sample

### 3.1 Initialize BleWiFiClient

CBPeripheral peripheral = ;

_mBleWiFiClient = [[BleWiFiClient alloc] initWithDevice:peripheral];;

### 3.2 Set the BleWiFiDelegate

_mBleWiFiClient.delegate = self;

### 3.3 Connect the Device

```
[_mBleWiFiClient connect];

//A successful connection is notified in the BleWiFiDelegate agent method

(void)onConnected:(BleWiFiClient )client {

}

//Discovery services and characteristics are notified in the BleWiFiDelegate agent method

(void)onServicesDiscovered:(BleWiFiClient )client {

    //Discover successful services and features

    [_mBleWiFiClient negotiateSecretKey];

}
```

### 3.4 Negotiate the data encryption key with Device

//Discover that the service and feature are successful, and begin key negotiation

```
[_mBleWiFiClient negotiateSecretKey];

//The negotiation results are notified in the BleWiFiDelegate agent method

(void)onNegotiateSecretKeyResult:(BleWiFiClient )client

Result:(BleWiFiBaseResult )result {

    if(result.status == STATUS_SUCCESS){

    //Successful negotiation

   	 [self onNegotiateSecretKeySuccess];

    }

    else{

    }

}
```

### 3.5 Began to distribution network

//The negotiation is successful and encryption of transmission network parameters is started

```
(void)onNegotiateSecretKeySuccess

{

    //The parameters of STA distribution network are constructed

    BleWiFiStaParams params = [[BleWiFiStaParams alloc] init];

    params.ssid = _txtSsid.text;

    params.password = _txtPassword.text;

    //Began to distribution network

    [_mBleWiFiClient configureSta:params];

}

//The mesh result is notified in the BleWiFiDelegate agent method

(void)onConfigureStaResult:(BleWiFiClient )client

Result:(BleWiFiConfigStaResult )result {

    if(result.status == STATUS_SUCCESS) {

        //WiFi: Mac address and Device IP address are displayed

        [self ShowMessage:[NSString stringWithFormat:@"Mac: %@",

        result.mac]];

        [self ShowMessage:[NSString stringWithFormat:@"IP Address: %@",

        result.ipAddress]];

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

