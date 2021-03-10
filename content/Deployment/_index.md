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

Navigate to the SharePoint company app catalog go to the Microsoft 365 admin center \&gt; Show all \&gt; SharePoint \&gt; Sites \&gt; Active sites or use this [link.](https://[YOUR\_TENANT]-admin.sharepoint.com/_layouts/15/online/AdminHome.aspx#/siteManagement/view/ALL%20SITES) Then in the &quot;Template&quot; column filter by &quot;App Catalog Site&quot; and click on the App Catalog Site URL.

![](/Deployment/images/01.png)

Some tenants do not have

In the App Catalog Site click on &quot;Apps for SharePoint&quot; \&gt; New \&gt; Choose Files \&gt; select the downloaded _permission-center-webpart.sppkg_ file \&gt; OK \&gt; then click &quot;Deploy&quot;.

![](RackMultipart20210310-4-1cduyo6_html_ed8604a9141b4d6b.jpg)

After the deployment, make sure the file is checked in. If you see an icon with a small green arrow you need to manually check the file in: Click the ellipsis (…) icon of the file \&gt; … \&gt; Advanced \&gt; Check In \&gt; OK

![](RackMultipart20210310-4-1cduyo6_html_4f62aba7eb0ad87c.jpg)

## 3) Deployment to a site collection app catalog

Navigate to the site collection you want to deploy the web part. Click on New \&gt; App

![](RackMultipart20210310-4-1cduyo6_html_20cff814f3545012.png)

Then &quot;From Your Organization&quot; and &quot;Permission Center web part.

![](RackMultipart20210310-4-1cduyo6_html_35828a7bce155f23.png)

Then in the upper right corner of the site, click on &quot;Edit&quot;.

![](RackMultipart20210310-4-1cduyo6_html_5baf66b545c96422.png)

Click on the &quot;plus&quot; of the section where you want to place the web part. Type &quot;perm&quot; and click on the Icon &quot;Permission Center&quot;. ![](RackMultipart20210310-4-1cduyo6_html_97a2aed1bbb1b24c.png)

Then republish the page.

![](RackMultipart20210310-4-1cduyo6_html_103dc336380a67b5.png)