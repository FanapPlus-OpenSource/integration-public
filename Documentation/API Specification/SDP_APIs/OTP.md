



![FanapPlus Logo](https://user-images.githubusercontent.com/32090767/46914641-2614f680-cfad-11e8-8607-74dec37b5f5d.png)

# OTP API

This document displays public specifications, samples and documentation for sending OTP (One Time Password) to end-users.

# Sending OTP
If an end-user wants to subscribe to a service, they will have to confirm the subscription request. Therefore, an activation code will be sent to the end-user & the developer will receive that code and send it to FanapPlus for confirmation.
In order to send the confirmation code (OTP) to end-user, the developer will have to call **Start** API. Next when the end-user enters the activation code in developer's program, **Commit** API should be called.

## Start API
This service will send a four-digit code to end-user.

### Start API Request

Method: POST
RequestUri:  https://api.sdp.fanap.plus/api/otp/start

The table below shows the parameters in request **Header**:

|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|SDP-Date|Date of request in UTC, [Iso 8601](https://en.wikipedia.org/wiki/ISO_8601) format <br> (`"yyyy-MM-ddTHH:mm:ss.fffZ"`)|e.g. 2019-01-26T11:00:42.364Z|
|SDP-ProductId|This ID should be acquired from [SDP](https://sdp.fanap.plus/), List of Products.  |e.g. 11035|
|SDP-Signature|Signed message* <br> [Which fields to sign?](#which-fields-to-sign)|"IMGFCgXPNIibooGTI6WhRxVcdc9sGBmZc05bAwyqYEib9<br>AOBVDHC0tvpE70MQz4Y+tpJiK2/JUksK86hxq2GBbfVTlP<br>Hi2YdaB7FuyHoRR5Cenp/8gA14+5qWTWA+uJBm8/0Rj8E/Pca<br>j8wV/wjkwVgEOMFfi/XvklgzAXwUXKU="|
|Content-Type|Type of the data which is being sent|application/json|

---
**NOTE** : `SDP-Signature` header is calculated using `SDP-ProductId` and `SDP-Date` headers:
```
SDP-Signature: Sign(SDP-ProductId#SDP-Date, YourPrivateKey)
```
---

The table below shows the parameters in request **Body**:

|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|phone|End-user's phone number |e.g. 9120000000|
|productId|This ID should be acquired from [SDP](https://sdp.fanap.plus/), List of Products.  |e.g. 11035|

#### Request Sample
```
Method: POST,
RequestUri: 'https://api.sdp.fanap.plus/api/otp/start'
Headers:
{
	SDP-Date: 2019-01-26T11:00:42.364Z
    SDP-ProductId: 11035
    SDP-Signature: YourSignature
    Content-Type: application/json; charset=utf-8
}
Body:
{
	"phone":"9120000000",
	"productId":11035
}
```
**NOTE**: The `otpId` field will be used in  [Commit](#commit-api) step.


### Start API Response

The table below shows the parameters in HTTP Response **Body**:

|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|OtpId|The OTP identifier code, this code should be kept for OTP confirmation.|6975be5c5a0541779af4d8d465e57b83          |

In case of successful response, you will receive following response body:
```
{
	"success":true,
	"result": {
		"otpId": "f72008d21b0a498aadf35482a319b81d"
	}
}
```

## Commit API
When this service is called, the end-user either gets subscribed to the subscription-based service or makes a purchase for On-Demand based services.

### Commit API Request

Method: POST
RequestUri: https://api.sdp.fanap.plus/api/otp/commit

The table below shows the parameters in request **Header**:

|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|SDP-Date|Date of request in UTC, [Iso 8601](https://en.wikipedia.org/wiki/ISO_8601) format <br> (`"yyyy-MM-ddTHH:mm:ss.fffZ"`)|e.g. 2019-01-26T11:00:42.364Z|
|SDP-ProductId|This ID should be acquired from [SDP](https://sdp.fanap.plus/), List of Products.  |e.g. 11035|
|SDP-Signature|Signed message* <br> [Which fields to sign?](#which-fields-to-sign)|"IMGFCgXPNIibooGTI6WhRxVcdc9sGBmZc05bAwyqYEib9<br>AOBVDHC0tvpE70MQz4Y+tpJiK2/JUksK86hxq2GBbfVTlP<br>Hi2YdaB7FuyHoRR5Cenp/8gA14+5qWTWA+uJBm8/0Rj8E/Pca<br>j8wV/wjkwVgEOMFfi/XvklgzAXwUXKU="|
|Content-Type|Type of the data which is being sent|application/json|

---
**NOTE** : `SDP-Signature` header is calculated using `SDP-ProductId` and `SDP-Date` headers:
```
SDP-Signature: Sign(SDP-ProductId#SDP-Date, YourPrivateKey)
```
---

The table below shows the parameters in request **Body**:

|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|OtpId|The OTP identifier code, this code should be kept for OTP confirmation.|6975be5c5a0541779af4d8d465e57b83          |
|Pin|OTP code entered by user|8807|

#### Request Sample
```
Method: POST,
RequestUri: 'https://api.sdp.fanap.plus/api/otp/commit'
Headers:
{
	SDP-Date: 2019-01-26T11:00:42.364Z
    SDP-ProductId: 11035
    SDP-Signature: YourSignature
    Content-Type: application/json; charset=utf-8
}
Body:
{
	"otpId":"f72008d21b0a498aadf35482a319b81d",
	"pin":"2511"
}
```
### Commit API Response

The table below shows the parameters in HTTP Response **Body**:


|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|refId|The reference identifier code. This code can be used to identify your HTTP request.|2602fcd79bb2412ab3f9cf57c17a43a3|

In case of successful response, you will receive following response body:
```
{
	"success":true,
	"result": {
		"refId": "2602fcd79bb2412ab3f9cf57c17a43a3"
	}
}
```
# Digital Signature

All requests sent to FanapPlus must be first signed by the developer. The signing process ensures that the service call is made by the developer herself. For further information refer to these links:

http://searchsecurity.techtarget.com/definition/digital-signature
https://www.docusign.com/how-it-works/electronic-signature/digital-signature/digital-signature-faq

## Generating RSA keys

In order to generate RSA keys, these steps should be followed:

 1. Download KeyGenerators.rar file from this link.
	[https://github.com/appson/payment-public/blob/master/v1.0.0/RSA%20Generator/src/Appson.Payment.KeyGenerator/bin/KeyGenerators.rar](https://github.com/appson/payment-public/blob/master/v1.0.0/RSA%20Generator/src/Appson.Payment.KeyGenerator/bin/KeyGenerators.rar)
 2. Extract file contents to the desired location.
 3. Open **Command Prompt** and change the directory to where you have stored the rar file contents.
 4. Type **Appson.Security.KeyGenerator.Console.exe** and press **Enter**.
 5. Choose the directory to store the set of keys.
 6. **Private Key** and **Public Key** files will be generated.
 7. Provide your **Public Key** in *xml* format to FanapPlus via a [ticket](https://ticket.fanap.plus/portal).
 

## Which fields to sign

In order to call any of FanapPlus's OTP APIs, you must sign as the following combination and store it in the `Signature`field of HTTP request body:

    AppId#TenantId#Date

In your signature, all the parameters which are being signed should have the exact same value as what they have in your request header/body.

So the structure of your request must be as follows:

HTTP Headers:

        Content-Type: application/json; charset=utf-8
        TenantId: your.tenant.id
        AppId: your-app-id
        //Additional headers go here

Body:

        {
            "Signature": Sign("your-app-id#your.tenant.id#2018-09-24T12:01:27.938Z", yourPrivateKey),
            "ServiceKey": "YourServiceKey",
            "Date":"2018-09-24T12:01:27.938Z",
            //Additional fields go here
        }
