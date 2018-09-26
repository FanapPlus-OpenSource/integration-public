
# IMI OTP API

This document displays public specifications, samples and documentation for sending OTP (One Time Password) to end-users.

# Sending OTP
If an end-user wants to subscribe to a service, their Mobile Network Operator is MCI, they need to confirm this request. Therefore, an activation code will be sent to the end-user & the developer will receive that code and send it to FanapPlus for confirmation.
In order to send the confirmation code (OTP) to end-user, the developer will have to call **Start** API. Next when the end-user enters the activation code in developer's program, **Commit** API should be called.

## Start API
This service will send a four-digit code to end-user.

### Start API Request

Method: POST
RequestUri: https://icp.sdp.fanap.plus/api/otp/start

The table below shows the parameters in request **Header**:


|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|Content-Type|Type of the data which is being sent.|application/json; charset=utf-8           |
|TenantId    |This ID should be acquired via a [ticket](https://ticket.fanap.plus/portal).  |2E06A1FF-09F0-4EBE-ACE5-ASD98W4ER98F|
|AppId       |This ID should be acquired via a [ticket](https://ticket.fanap.plus/portal).  |345J6JSD-GJ0S-D82N-SDF8-GV50S3898345

The table below shows the parameters in request **Body**:

|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|Date|Date of request in UTC, [Iso 8601](https://en.wikipedia.org/wiki/ISO_8601) format <br> (`"yyyy-MM-ddTHH:mm:ss.fffZ"`)|2018-09-24T07:41:32.443Z|
|PhoneNumber|End-user's phone number |09121111111           |
|ServiceKey|The service identifier code provided by FanapPlus to CP |e61e19e1070e4d3293cf3f7e5ba22267|
|Signature|Signed message  |"IMGFCgXPNIibooGTI6WhRxVcdc9sGBmZc05bAwyqYEib9AOBVDHC0tvpE70MQz4Y+tpJiK2/JUksK86hxq2GBbfVTlPHi2YdaB7FuyHoRR5Cenp/8gA14+5qWTWA+uJBm8/0Rj8E/Pcaj8wV/wjkwVgEOMFfi/XvklgzAXwUXKU="|

#### Request Sample

    Method: POST, RequestUri: 'https://icp.sdp.fanap.plus/api/otp/start', Version: 1.1, Content: System.Net.Http.StringContent, Headers:
    {
      Content-Type: application/json; charset=utf-8
      TenantId: your.tenant.id
      AppId: 5812d7c8bb9c4b798b23316749ef19eb
    }
    {
    	"Date":"2018-09-24T07:41:32.443Z",
    	"PhoneNumber":"09120000000",
    	"ServiceKey":"63b01900e9c447e4930ce8ab0969e6f3",
    	"Signature":"OOfREvnE9V720y5bxzw1QIJwf6NgRcbur334iZeRC6fDMKMIxZAWPi/JfUQbWIFT/JAkNme5BnFtKlWXPQhjO4o64CpaooN0MqkaLBHhhiCWL7G843Z8uVtEnE/zNjHDpJNKMvXX0GNY9yXyZcnKV0GganJN48Rzk79GXGogrCvCF+vSgN3bo/dHwakSTASiSXALYIU3SyG0y9o7QpGri+SXYZT7b38kGcNcI4AA0ScDHKApVtmz6VbNe5thULq+xaKSMR68okiyyrt/8ghLYH0zi9vdJ0F/K/FAEaetibLFDUO8iTQJ2VBuMVDnkd9nbkjN+AtIXiGi//jKowrslQ=="
    }
    
### Start API Response

The table below shows the parameters in HTTP Response **Body**:


|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|OtpId|The OTP identifier code, this code should be kept for OTP confirmation.|6975be5c5a0541779af4d8d465e57b83          |
|RequestId|The request identifier code|f74053ab0a62429c8b636619d8a4badc|



#### Response Sample
    
    StatusCode: 200, ReasonPhrase: 'OK', Version: 1.1, Content: System.Net.Http.StreamContent, Headers:
    {
      Pragma: no-cache
      X-SourceFiles: =?UTF-8?B?RDpcZ2l0XENoYXJpdHlcSUNQU2VydmljZVxCYWJhUGF6UHJvamVjdFxhcGlcb3RwXHN0YXJ0?=
      Cache-Control: no-cache
      Date: Mon, 24 Sep 2018 07:41:42 GMT
      Server: Microsoft-IIS/10.0
      X-AspNet-Version: 4.0.30319
      X-Powered-By: ASP.NET
      Content-Length: 91
      Content-Type: application/json; charset=utf-8
      Expires: -1
    }
    {
    "OtpId":"5f8db2e9e3c94532b4648c16cd52be37",
    "RequestId":"370b5cae1d614906bb9dd394a5bb9559"
	}


## Commit API
When this service is called, the end-user either gets subscribed to the subscription-based service or makes a purchase for On-Demand based services.

### Commit API Request

Method: POST
RequestUri: https://icp.sdp.fanap.plus/api/otp/commit

The table below shows the parameters in request **Header**:


|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|Content-Type|Type of the data which is being sent.|application/json; charset=utf-8           |
|TenantId    |This ID should be acquired via a [ticket](https://ticket.fanap.plus/portal). |2E06A1FF-09F0-4EBE-ACE5-ASD98W4ER98F|
|AppId       |This ID should be acquired via a [ticket](https://ticket.fanap.plus/portal). |345J6JSD-GJ0S-D82N-SDF8-GV50S3898345

The table below shows the parameters in request **Body**:

|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|Date|Date of request in UTC, [Iso 8601](https://en.wikipedia.org/wiki/ISO_8601) format <br> (`"yyyy-MM-ddTHH:mm:ss.fffZ"`)|2018-09-24T07:43:23.045Z|
|OtpId|The OTP identifier code, this code should acquired in response of Start API.|6975be5c5a0541779af4d8d465e57b83          |
|Pin|OTP code entered by user|"8807"|
|ServiceKey|The service identifier code provided by FanapPlus to CP |e61e19e1070e4d3293cf3f7e5ba22267|
|Signature|Signed message  |"IMGFCgXPNIibooGTI6WhRxVcdc9sGBmZc05bAwyqYEib9<br>AOBVDHC0tvpE70MQz4Y+tpJiK2/JUksK86hxq2GBbfVTlP<br>Hi2YdaB7FuyHoRR5Cenp/8gA14+5qWTWA+uJBm8/0Rj8E/Pca<br>j8wV/wjkwVgEOMFfi/XvklgzAXwUXKU="

#### Request Sample

    Method: POST, RequestUri: 'https://icp.sdp.fanap.plus/api/otp/commit', Version: 1.1, Content: System.Net.Http.StringContent, Headers:
    {
      Content-Type: application/json; charset=utf-8
      TenantId: your.tenant.id
      AppId: 5812d7c8bb9c4b798b23316749ef19eb
    }
    {
    "Date":"2018-09-24T07:43:23.045Z",
    "OtpId":"5f8db2e9e3c94532b4648c16cd52be37",
    "Pin":"8077",
    "ServiceKey":"63b01900e9c447e4930ce8ab0969e6f3",
    "Signature":"J8/rSZlOssC/o34sEJdKlVjiieLhfS4T2hcmqHUqPyXLSso39jihFzLysWhHuNs1BjalDnak4ocNgBSckMR3/tqCTrmqStmA0impWe65cHJdGC4uV8/YuOxNGlWOpRad149j0JcARDWyISW6bZb1Abh8ZGOnf9SYUzWrrwQ3v4JZzoUL+pLjHm1XvYyHokw3vyU1FV+NPQVvhH6xTvoiU15GHCkPZ3aGkkso6wa/nURUOqy7s0esVwXKBTukO9TCut43s1h6qgIgeBniL82VUa6umyfe3b58sIs3E+6rdJnKH07rZbDmwGfJgdk8m5dc8pEpGa2aY03vCiCXR2OWWQ=="
    }
    
### Commit API Response

The table below shows the parameters in HTTP Response **Body**:


|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|RequestId|The request identifier code|f74053ab0a62429c8b636619d8a4badc|



#### Response Sample
    
        StatusCode: 200, ReasonPhrase: 'OK', Version: 1.1, Content: System.Net.Http.StreamContent, Headers:
    {
      Pragma: no-cache
      X-SourceFiles: =?UTF-8?B?RDpcZ2l0XENoYXJpdHlcSUNQU2VydmljZVxCYWJhUGF6UHJvamVjdFxhcGlcb3RwXGNvbW1pdA==?=
      Cache-Control: no-cache
      Date: Mon, 24 Sep 2018 07:43:36 GMT
      Server: Microsoft-IIS/10.0
      X-AspNet-Version: 4.0.30319
      X-Powered-By: ASP.NET
      Content-Length: 48
      Content-Type: application/json; charset=utf-8
      Expires: -1
    }
    {
    "RequestId":"e4f8a523862d4b1a912be2a71ae3ed38"
    }

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
 7. Provide your **Public Key** in *xml* format to FanapPlus.
 

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
