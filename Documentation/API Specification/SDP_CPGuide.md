

![FanapPlus Logo](https://user-images.githubusercontent.com/32090767/46914641-2614f680-cfad-11e8-8607-74dec37b5f5d.png)

# SDP User Manual for Content Providers

## Table of Contents
1. [Introduction](#introduction)
2. [Login](#login)
3. [Reporting Dashboard](#reporting-dashboard)
4. [Technical Documents](#technical-documents)
5. [Content Providers](#content-providers)
6. [Users](#users)
7. [Bulk Management](#bulk-management)
8. [Service Management](#service-management)
9. [Product Management](#product-management)
10. [News Broadcasting](#news-broadcasting)
 

## Introduction

Fanap Plus Service Delivery Platform is platform that presents service delivery architecture to businesses who are utilizing telecommunication services, connecting them to Mobile Network Operators. However this explanation is specific to Fanap Plus and there is no standard definition of SDP in industry and different players define its characteristics in different ways. Yet the main feature of SDP is that it requires a complete integration of IT capabilities and the creation of services that cross technology and network boundaries. 
Fanap Plus is offering telecommunications services such as Messaging services as well as non-telecommunication ones such as Score & Credit Calculations, Authentication and Reporting services.
The purpose of this platform is to enable rapid development and deployment of all services.


## Login
 Use [this link](https://sdp.fanap.plus/account/login) to login to Fanap Plus SDP by using credentials sent to you via email. At the top of this page, you should choose your company name.
You can check the "Remember Me" checkbox so that the next time you visit the website, the browser automatically fills up the password field for you.
![Login Box](https://user-images.githubusercontent.com/32090767/48659440-927c8d00-ea66-11e8-9c84-c15680bf6d7e.jpg)
## Reporting Dashboard

![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48704576-2dfb3280-ec0c-11e8-82bb-46c8627c286f.jpg)

### Search Box

The first page that you will be directed to is the reporting dashboard. 

In the __Search Box__, you can select the *Service / Services Name* and the *Time Range* for the requested reports. After filling in the required fields, press *View* button 
In the bottom part of the page, where the reports will be visible, there are different __Report Type__ tabs to select. The selected __Report Type__ by default is of *Subscription* type, however other types of reports such as *Revocation*, *Income* and *Messages* can be also selected by switching between tabs.
* The maximum selectable time range is 6 months.
* The end date should can be until yesterday.

![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48660215-80edb200-ea73-11e8-8491-e457e150a2ff.jpg)

### Pie Charts
After the search parameters are chosen, a pie chart will apear. Above the pie chart the __Total Amount__ of the *Report Type* selected is written. Below inside the pie chart the percentage of different subscriber types is available on mouse hover.
![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48692887-df8a6b80-ebec-11e8-8a18-8abdb8d43384.jpg)

### Line Graphs
Another element of the __Reporting Dashboard__ is a line graph which shows the amount for each type of subscriber on a specific date. By hovering on the point of the graphs, the number in its written form will be visible.
![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48693394-90ddd100-ebee-11e8-87c3-739273c23da0.jpg)

### Data Table
Lastly you can view the data table in the bottom part of the __Reporting Dashboard__. In this table you can view the data related to a service/services and the option of exporting the data to CSV format is also available.

![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48706164-a6fc8900-ec10-11e8-91ad-df57a3f600bb.jpg)

## Technical Documents

Technical Documents section which is accessible from the menu, contains Fanap Plus's __technical__ documents. When this icon is clicked, you will be directed to the main page of the Technical Documents and a list of available documents will be visible.

![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48704578-2e93c900-ec0c-11e8-8f36-5e29a85c241b.jpg)
The main page of Technical Documents consists of a Tree List as you can see below. Various categories of documents or the documents themselves can be added to this section both individually or as subsets.

![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48706781-846b6f80-ec12-11e8-8386-1ba5e0f8f204.jpg)

## Users
You can create users in SDP and share the credentials with them for log-in.

![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48704567-2d629c00-ec0c-11e8-9547-2801ef4a144a.jpg)


![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48759001-12009b00-ecb7-11e8-86bc-d2e0a180dee0.jpg)

## Bulk Management
One of the main features of SDP is Bulk / Campaign Management. In this section, users are able to create user segments, choose tags, schedule times to send bulk messages to them and more.

### User Segmentation
The first step in sending bulk messages to users is to create a __User Segment__. 


![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48704569-2d629c00-ec0c-11e8-9dcd-63718ab70d41.jpg)

A User Segment can either be created by using *Account IDs* or *User Phone Numbers*. Account ID is a hashed string which uniquely identifies each user who signs in using Fanap Plus Identity. Another way of acquiring Account IDs is to receive it in *Messaging* requests. After choosing the user type, a name should be assigned to the segment and lastly a CSV file containing user information (phone number / Account ID) should be uploaded by the user. There is also a sample user information file ready to be downloaded which contains sample phone numbers or AccounIDs and shows the right format of the file to be uploaded.

![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48760108-4cb80280-ecba-11e8-84ee-faddc84df08c.jpg)
After creating the segment, by clicking on the eye icon, the user can view the segment information and add custom tags to the segment. The tags will be stored for each message sent to end-users.

![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48764181-357e1280-ecc4-11e8-80b1-18cc31cb0891.jpg)

### Bulk Request
The second step in Bulk Management is to schedule for a bulk to be sent to a specific segment. Note that the bulk will only be sent if the administrator approves it.

![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48704568-2d629c00-ec0c-11e8-9bc4-faf7934bf89d.jpg)

![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48764944-4fb8f000-ecc6-11e8-83fe-e06be3168093.jpg)

## Service Management

![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48704577-2e93c900-ec0c-11e8-87df-9c0d42b74919.jpg)
In order to map Mobile Network Operator services to their owners, a.k.a CPs, __Service Management__ should take place. You can view your AppID and Services in this section in the form of a list.
Note that an AppID is a hashed string which uniquely identifies each application. The owner of the AppID is previously identified by Fanap Plus Identity using their TenantID and Each Tenant can have infinite number of applications.​

## Product Management

When services are created and approved by the administrator, the user can create various products connected to their services.

![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48704575-2dfb3280-ec0c-11e8-9a0c-ebe588fcab9d.jpg)

On the main page of __Product Management__ a list of existing products is available. Note that the list has a default filter and it only displays the active products, however this filter can be removed if necessary.
As the administrator, when creating a product, the first step should be to choose the Content Provider. Next, one of the available templates should be chosen:

### IMI 3G Template


![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48768004-4717e800-eccd-11e8-8e12-9cd343c8c211.jpg)

Products created by using IMI Default Template will send welcome, parting, invalid keyword and help messages to end-users. The following fields should be filled out:

 - Product Name
 - Service Name: One of the approved services can be selected.
 - Welcome Message: The message that will be sent to end-users when they subscribe to the selected service.
 - Parting Message: The message that will be sent to end-users when they revoke their subscription to the selected service.
 - Invalid Keyword Message: The message that will be sent to end-users when they send an invalid keyword to the selected service's short code.
 - Help Message: The message that will be sent to end-users when they send an empty message to the selected service's short code.
 - Subscription Keywords
 - Revocation Keywords
 
### Pardis 3G Template


![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48768221-d91ff080-eccd-11e8-87f6-2f387e8b5056.jpg)

Products created by using Pardis 3G Template will send welcome, parting, invalid keyword and help messages to end-users. The following fields should be filled out:

 - Product Name
 - Service Name: One of the approved services can be selected.
 - Welcome Message: The message that will be sent to end-users when they subscribe to the selected service.
 - Parting Message: The message that will be sent to end-users when they revoke their subscription to the selected service.
 - Invalid Keyword Message: The message that will be sent to end-users when they send an invalid keyword to the selected service's short code.
 - Help Message: The message that will be sent to end-users when they send an empty message to the selected service's short code.
 - Subscription Keywords
 - Revocation Keywords

### Pardis 2G Template


![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48768639-d5409e00-ecce-11e8-97fd-c5976e1d9b1a.jpg)

Products created by using Pardis 3G Template has 3 capabilities; it can send welcome, parting, invalid keyword and help messages to end-user. In addition, it can also send premium and free content to the subscribers. The following fields should be filled out:

Daily Content (Free & Premium) :

 - Start Time
 - End Time
 - Add file : the file can be both uploaded or added manually
In order to delete records from this section, each record must be removed individually.
The Date of daily content to be send should be greater than today.

Sending Step:
 - Product Name
 - Service Name: One of the approved services can be selected.
 - Welcome Message: The message that will be sent to end-users when they subscribe to the selected service.
 - Parting Message: The message that will be sent to end-users when they revoke their subscription to the selected service.
 - Invalid Keyword Message: The message that will be sent to end-users when they send an invalid keyword to the selected service's short code.
 - Help Message: The message that will be sent to end-users when they send an empty message to the selected service's short code.
 - Subscription Keywords
 - Revocation Keywords
 
 
## News Broadcasting

In this section the administrator is able to broadcast news and target the service owners.
![Menu-ReportingDashboard](https://user-images.githubusercontent.com/32090767/48704573-2dfb3280-ec0c-11e8-9de8-f12d451de383.jpg)
You can view the news broadcasted by FanapPlus in this section before they reach the expiry time.
