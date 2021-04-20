---
title: "Deployment instructions"
date: 2021-03-01T14:38:53-06:00
draft: false
weight: 01
---
Karsten Held, Samuel Gross, 10.02.2021

### 1) Download

- Download the zipped web part package file **permission-center-webpart.sppkg** from GitHub:
[Latest release](https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part/releases/download/V1.1.0.0/SharePoint-Package_sppkg.zip) / 
[All releases](https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part/releases).

- Unzip the SPPKG file. Do not rename this file. The filename has to match the package name.

### 2) Deployment to the global app catalog

- Navigate to your App Catalog site. If you don't know the URL of your App Catalog site, follow these steps:
- Navigate to the SharePoint company app catalog
- Go to the Microsoft 365 admin center > Show all > SharePoint > Sites > Active sites or use this link: 
`https://[YOUR_TENANT]-admin.sharepoint.com/_layouts/15/online/AdminHome.aspx#/siteManagement/view/ALL%20SITES`
- If you don't have an App catalog, make sure to create one first.
- In the "Template" column, filter by "App Catalog Site" and click on the App Catalog Site URL.

![](/Deployment/images/01.png)

- In the App Catalog Site click on "Apps for SharePoint" > New > Choose Files > select the downloaded **permission-center-webpart.sppkg** file > OK > then click "Deploy".

![](/Deployment/images/02.png)


- After the deployment, make sure the file is checked in. If you see an icon with a small green arrow you need to manually check the file in: Click the ellipsis (…) icon of the file > … > Advanced > Check In > OK

![](/Deployment/images/03.png)


### 3) Deployment to a site collection app catalog

- Navigate to the site collection you want to deploy the web part. Click on New > App

![](/Deployment/images/04.png)


- Go to "From Your Organization" > "Permission Center web part".

![](/Deployment/images/05.png)


- In the upper right corner of the site, click on "Edit".

![](/Deployment/images/06.png)


- Click on the "plus" in the section where you want to place the web part. 
- Type "perm" and click on the icon of the "Permission Center". 

![](/Deployment/images/07.png)

- Republish the page.

![](/Deployment/images/08.png)
