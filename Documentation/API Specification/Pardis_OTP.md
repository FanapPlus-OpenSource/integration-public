![FanapPlus Logo](https://user-images.githubusercontent.com/32090767/46914641-2614f680-cfad-11e8-8607-74dec37b5f5d.png)

# Pardis OTP API

This document displays public specifications, samples and documentation for sending OTP (One Time Password) to end-users.

# Sending OTP
If an end-user wants to subscribe to a service, their Mobile Network Operator is MCI, they need to confirm this request. Therefore, an activation code will be sent to the end-user & the developer will receive that code and send it to FanapPlus for confirmation.
In order to send the confirmation code (OTP) to end-user, the developer will have to call **Start** API. Next when the end-user enters the activation code in developer's program, **Commit** API should be called.

## Start API
This service will send a four-digit code to end-user.

### Start API Request

Method: POST
RequestUri: https://sscp.sdp.fanap.plus/api/Subscription/grant/start

The table below shows the parameters in request **Header**:


|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|Content-Type|Type of the data which is being sent.|application/json; charset=utf-8           |
|TenantId    |This ID should be acquired via a [ticket](https://ticket.fanap.plus/portal).  |your.tenant.id|
|AppId       |This ID should be acquired via a [ticket](https://ticket.fanap.plus/portal).  |your-app-id

The table below shows the parameters in request **Body**:

|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|Date|Date of request in UTC, [Iso 8601](https://en.wikipedia.org/wiki/ISO_8601) format <br> (`"yyyy-MM-ddTHH:mm:ss.fffZ"`)|2018-09-24T07:41:32.443Z|
|PhoneNumber|End-user's phone number |09120000000           |
|ServiceKey|The service identifier code provided by FanapPlus to CP |63b01900e9c447e4930ce8ab0969e6f3|
|Signature|Signed message  |"IMGFCgXPNIibooGTI6WhRxVcdc9sGBmZc05bAwyqYEib9AOBVDHC0tvpE70MQz4Y+tpJiK2/JUksK86hxq2GBbfVTlPHi2YdaB7FuyHoRR5Cenp/8gA14+5qWTWA+uJBm8/0Rj8E/Pcaj8wV/wjkwVgEOMFfi/XvklgzAXwUXKU="|

#### Request Sample

    Method: POST, RequestUri: 'https://sscp.sdp.fanap.plus/api/Subscription/grant/start', Version: 1.1, Content: System.Net.Http.StringContent, Headers:
    {
      Content-Type: application/json; charset=utf-8
      TenantId: your.tenant.id
      AppId: your-app-id
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
|Response|Indicates the state of the request. If the state is zero, the response is successful. Any other value represents an operator error.|0          |
|correlationId|The request identifier code|973358ae413e4379881476cbd3486aa0|
|success|The overall state of the request|true/false|



#### Response Sample
    
    StatusCode: 200, ReasonPhrase: 'OK', Version: 1.1, Content: System.Net.Http.NoWriteNoSeekStreamContent, Headers:
    {
      Date: Mon, 24 Sep 2018 12:02:27 GMT
      Transfer-Encoding: chunked
      Server: Kestrel
      X-SourceFiles: =?UTF-8?B?RDpcZ2l0XFNEUC1TQ01cc3JjXFdlYlxhcGlcU3Vic2NyaXB0aW9uXGdyYW50XHN0YXJ0?=
      X-Powered-By: ASP.NET
      Content-Type: application/json; charset=utf-8
    }
    {
	"response":0,
    "correlationId":"973358ae413e4379881476cbd3486aa0",
    "success":true
    }


## Commit API
When this service is called, the end-user either gets subscribed to the subscription-based service or makes a purchase for On-Demand based services.

### Commit API Request

Method: POST
RequestUri: https://sscp.sdp.fanap.plus/api/Subscription/grant/commit

The table below shows the parameters in request **Header**:


|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|Content-Type|Type of the data which is being sent.|application/json; charset=utf-8           |
|TenantId    |This ID should be acquired via a [ticket](https://ticket.fanap.plus/portal). |your.tenant.id|
|AppId       |This ID should be acquired via a [ticket](https://ticket.fanap.plus/portal). |your-app-id

The table below shows the parameters in request **Body**:

|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|Date|Date of request in UTC, [Iso 8601](https://en.wikipedia.org/wiki/ISO_8601) format <br> (`"yyyy-MM-ddTHH:mm:ss.fffZ"`)|2018-09-24T07:43:23.045Z|
|PhoneNumber|End-user's phone number |09120000000           |
|CorrelationId|The OTP identifier code, this code should acquired in response of Start API.|6975be5c5a0541779af4d8d465e57b83          |
|Token|OTP code entered by user|"3007"|
|ServiceKey|The service identifier code provided by FanapPlus to CP |63b01900e9c447e4930ce8ab0969e6f3|
|Signature|Signed message  |"IMGFCgXPNIibooGTI6WhRxVcdc9sGBmZc05bAwyqYEib9<br>AOBVDHC0tvpE70MQz4Y+tpJiK2/JUksK86hxq2GBbfVTlP<br>Hi2YdaB7FuyHoRR5Cenp/8gA14+5qWTWA+uJBm8/0Rj8E/Pca<br>j8wV/wjkwVgEOMFfi/XvklgzAXwUXKU="

#### Request Sample

    Method: POST, RequestUri: 'https://sscp.sdp.fanap.plus/api/Subscription/grant/commit', Version: 1.1, Content: System.Net.Http.StringContent, Headers:
    {
      Content-Type: application/json; charset=utf-8
      TenantId: your.tenant.id
      AppId: your-app-id
    }
    {
    "ServiceKey":"63b01900e9c447e4930ce8ab0969e6f3",
    "PhoneNumber":"9120000000",
    "CorrelationId":"973358ae413e4379881476cbd3486aa0",
    "Token":"3007",
    "Date":"2018-09-24T12:14:20.453Z",
    "Signature":"gbvNF+Gpi+uO5B0DSt5i3ZT5G/3ogy3X2nuh3sYxgaki/E6Od7dw0V0V/T/rUSwVCBxUXel9FlH7q0YLGijuWjDU6zc1tqsymNYBbZiehhgPV0pcHJzdENjNVH8OsaUb7YC972ogM05I5FAVZNpOhSGwgqcuWM3MUh2lGNhXRzrIhno5DI4B/4DBH/kpOFQFBgutCQCE9Mfn0X7Jh/P+FKaNVkYJfs58Cl99Q94wTgtZz5hQyEFrcyTPSMg8Qn7opmAZ7r52j/eE+EqYctyO/yHxgbyP3hivdcisbejPSbMchKExYTXx4IGxBo2kOglu9UwInhoBfdroJ4IwXphcbQ=="
    }

    
### Commit API Response

The table below shows the parameters in HTTP Response **Body**:


|Name            |Description                    |Example                       |
|----------------|-------------------------------|-----------------------------|
|Response|Indicates the state of the request. If the state is zero, the response is successful. Any other value represents an operator error.|0          |
|success|The overall state of the request|true/false|




#### Response Sample
    
    

    StatusCode: 200, ReasonPhrase: 'OK', Version: 1.1, Content: System.Net.Http.NoWriteNoSeekStreamContent, Headers:
    {
      Date: Mon, 24 Sep 2018 12:14:37 GMT
      Transfer-Encoding: chunked
      Server: Kestrel
      X-SourceFiles: =?UTF-8?B?RDpcZ2l0XFNEUC1TQ01cc3JjXFdlYlxhcGlcU3Vic2NyaXB0aW9uXGdyYW50XGNvbW1pdA==?=
      X-Powered-By: ASP.NET
      Content-Type: application/json; charset=utf-8
    }
    {
    "response":0,
    "success":true
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
 7. Provide your **Public Key** in *xml* format to FanapPlus in the form of a [ticket](https://ticket.fanap.plus/portal).
 

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
