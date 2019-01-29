




![FanapPlus Logo](https://user-images.githubusercontent.com/32090767/46914641-2614f680-cfad-11e8-8607-74dec37b5f5d.png)

# Subscription Verification

This document displays public specifications, samples and documentation for verifying an end-user is subscribed to a service. Please note that this API only responds to a user's subscription on Pardis platform services.

## Verify Subscription API Request
Method: GET
RequestUri:  https://api.sdp.fanap.plus/api/subscription/verification/{phone}/product/{productId}

The table below shows the parameters in request **Header**:

|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|SDP-Date|Date of request in UTC, [Iso 8601](https://en.wikipedia.org/wiki/ISO_8601) format <br> (`"yyyy-MM-ddTHH:mm:ss.fffZ"`)|e.g. 2019-01-26T11:00:42.364Z|
|SDP-ProductId|This ID should be acquired from [SDP](https://sdp.fanap.plus/), List of Products.  |e.g. 11035|
|SDP-Signature|Signed message* <br> [Which fields to sign?](#which-fields-to-sign)|"IMGFCgXPNIibooGTI6WhRxVcdc9sGBmZc05bAwyqYEib9<br>AOBVDHC0tvpE70MQz4Y+tpJiK2/JUksK86hxq2GBbfVTlP<br>Hi2YdaB7FuyHoRR5Cenp/8gA14+5qWTWA+uJBm8/0Rj8E/Pca<br>j8wV/wjkwVgEOMFfi/XvklgzAXwUXKU="|

---
**NOTE** : `SDP-Signature` header is calculated using `SDP-ProductId` and `SDP-Date` headers:
```
SDP-Signature: Sign(SDP-ProductId#SDP-Date, YourPrivateKey)
```
---
## Verify Subscription API Response

### Successful Response
In case of successful response, you will receive the following response:
```
{
	"success":true,
	"result":
	{
		"refId":"934c824f91614cb1bfbf315407d39fe6",
		"isSubscribed":true
	}
}
```
### Unsuccessful Response
If you receive HTTP status code 401, it means that we couldn't verify your signature. The error has following HTTP body:
```
{
	"success":false,
	"error":
	{
		"code":1019,
		"message":"HTTP header is not found: SDP-Date"
	}
}
```
In other cases you will receive HTTP status code 400 and response body will have following HTTP body:
```
{
	"success": false,
	"error": 
	{
		"code": 1011,
		"validationErrors": 
		[
			{
				"message": "Can not find any otp record for OtpId: e13db7c996da417f9db160d555aec838",
				"members": null
			}
		]
	}
}
```

### Error List
| Error Name | Error Code|
|----------- |:--------:|
|ProductNotFound | 1001 |
|TenantNotFound | 1002 |
|TenantPublicKeyIsNotSet | 1003 |
|SignatureIsNotValid | 1004 |
|ProductDefinitionIsNotValid | 1005 |
|ServiceNotFound | 1006 |
|MobileOperatorServiceNotFound | 1007 |
|GhasedakServiceError | 1008 |
|StartCommitNotFound | 1009 |
|RequestDateTimeIsNotValid | 1010 |
|RequestDateTimeIsOutOfRange | 1011 |
|SignatureIsRequired | 1012 |
|InvalidPin | 1013 |
|InvalidOtpId | 1014 |
|InvalidPhone | 1015 |
|OtpIdAlreadyUsed | 1016 |
|ProductIdIsNotValid | 1017 |
|InvalidProductId | 1018 |
|HeaderNotFound | 1019 |

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
