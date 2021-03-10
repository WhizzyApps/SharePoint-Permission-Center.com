---
title: "Deployment"
date: 2021-03-01T14:38:53-06:00
draft: false
---

# Deployment instructions

## 1) Download

Download the web part package file _permission-center-webpart.sppkg_ from [Github](https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part/releases). Do not rename the file. The filename has to match the package name.

## 2) Deployment to the global app catalog

Navigate to your App Catalog site. If you don&#39;t know the URL of your App Catalog site, follow these steps:

Navigate to the SharePoint company app catalog go to the Microsoft 365 admin center > Show all > SharePoint > Sites > Active sites or use this [link.](https://[YOUR\_TENANT]-admin.sharepoint.com/_layouts/15/online/AdminHome.aspx#/siteManagement/view/ALL SITES) Then in the &quot;Template&quot; column filter by &quot;App Catalog Site&quot; and click on the App Catalog Site URL.

![](/Deployment/images/01.png)

If you don’t have an App catalog, make sure to create one first.

In the App Catalog Site click on &quot;Apps for SharePoint&quot; > New > Choose Files > select the downloaded _permission-center-webpart.sppkg_ file > OK > then click &quot;Deploy&quot;.

![](/Deployment/images/02.png)

After the deployment, make sure the file is checked in. If you see an icon with a small green arrow you need to manually check the file in: Click the ellipsis (…) icon of the file > … > Advanced > Check In > OK

![](/Deployment/images/03.png)

## 3) Deployment to a site collection app catalog

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