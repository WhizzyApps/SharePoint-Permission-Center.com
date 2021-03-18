---
title: "Deployment"
date: 2021-03-01T14:38:53-06:00
draft: false
weight: 01
---

### Deployment instructions

#### 1) Download

Download the zipped web part package file _permission-center-webpart.sppkg_ from [Github](https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part/releases). Unzip the SPPKG file. Do not rename this file. The filename has to match the package name.

#### 2) Deployment to the global app catalog

Navigate to your App Catalog site. If you don't know the URL of your App Catalog site, follow these steps:

**Navigate to the SharePoint company app catalog**

Go to the Microsoft 365 admin center > Show all > SharePoint > Sites > Active sites or use this link: 
https://[YOUR_TENANT]-admin.sharepoint.com/_layouts/15/online/AdminHome.aspx#/siteManagement/view/ALL%20SITES

If you don't have an App catalog, make sure to create one first.

Then in the "Template" column, filter by "App Catalog Site" and click on the App Catalog Site URL.

![](/Deployment/images/01.png)

In the App Catalog Site click on "Apps for SharePoint" > New > Choose Files > select the downloaded _permission-center-webpart.sppkg_ file > OK > then click "Deploy".

![](/Deployment/images/02.png)


After the deployment, make sure the file is checked in. If you see an icon with a small green arrow you need to manually check the file in: Click the ellipsis (…) icon of the file > … > Advanced > Check In > OK

![](/Deployment/images/03.png)


#### 3) Deployment to a site collection app catalog

Navigate to the site collection you want to deploy the web part. Click on New > App

![](/Deployment/images/04.png)


Then &quot;From Your Organization&quot; and &quot;Permission Center web part.

![](/Deployment/images/05.png)


Then in the upper right corner of the site, click on &quot;Edit&quot;.

![](/Deployment/images/06.png)


Click on the &quot;plus&quot; of the section where you want to place the web part. Type &quot;perm&quot; and click on the Icon &quot;Permission Center&quot;. 
![](/Deployment/images/07.png)


Then republish the page.

![](/Deployment/images/08.png)
