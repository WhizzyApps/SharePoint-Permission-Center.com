---
title: "Deployment instructions"
date: 2021-12-01
draft: false
weight: 01
---
Karsten Held, Samuel Gross, 01.12.2021


### 1) Download

- Download the zipped web part package file **permission-center-webpart.sppkg** from GitHub:
{{< rawhtml >}}
    <a style="align-self: flex-start;" href="https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part/releases/download/V1.1.0/SharePoint-Package_sppkg.zip">Latest release/</a>
    <a style="align-self: flex-start;" href="https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part/releases" target="_blank">All releases</a>
{{</ rawhtml >}}
- Unzip the SPPKG file. Do not rename this file. The filename has to match the package name.


### 2) Deployment to the global app catalog

#### A) Go to your App Catalog site

- Check if you have an App Catalog site by navigating to it. If you don't know the URL of your App Catalog site, follow one of these steps:
- Option a) Use this link: 
`https://[YOUR_TENANT]-admin.sharepoint.com/_layouts/15/online/AdminHome.aspx#/siteManagement/view/ALL%20SITES`

- Option b) Navigate to the SharePoint company App Catalog: 
  - Go to the Microsoft 365 admin center > Show all > SharePoint > Sites > Active sites
  - In the "Template" column, filter by "App Catalog Site" and click on the App Catalog Site URL.

![](/Deployment/images/04.png)

- If you don't have an App Catalog, make sure to create one first under point B). Else, go to point C).

#### B) Create an App Catalog site - optional


- In the SharePoint admin center, navigate through More features > Apps > open

![](/Deployment/images/01.png)

- Go to App Catalog:

![](/Deployment/images/02.png)

- Create a new app catalog site > OK:

![](/Deployment/images/03.png)

- On the next site, fill out the data > OK

#### C) Deploy the webpart to the global app catalog 

- In the App Catalog Site click on "Apps for SharePoint" > New > Choose Files > select the downloaded **permission-center-webpart.sppkg** file > OK > then click "Deploy".

![](/Deployment/images/05.png)


- After the deployment, make sure the file is checked in. If you see an icon with a small green arrow you need to manually check the file in: Click the ellipsis (…) icon of the file > … > Advanced > Check In > OK

![](/Deployment/images/06.png)


### 3) Grant permissions

The web part must have access to the Microsoft Graph API. To get access a SharePoint administrator has to give the permissions.
The permissions needed are called "Directory.AccessAsUser.All". It allows the app to have the same access to information in the directory as the signed-in user. See Microsoft [documentation](https://docs.microsoft.com/en-us/graph/permissions-reference).

To grant access, follow the steps shown in the picture below:

1. Go to the SharePoint admin center > Advanced > API access
2. Click under "Pending requests" on the Package "Permission Center web part" with the permission "Directory.AccessAsUser.All"
3. Click Approve, then Approve, then find it under "Approved requests"

![](/Deployment/images/07.png)
 

### 4) Deployment to a site collection app catalog

- Navigate to the site collection you want to deploy the web part. Click on New > App

![](/Deployment/images/08.png)


- Go to "From Your Organization" > "Permission Center web part".

![](/Deployment/images/09.png)


### 5) Add webpart to your site

- On your site, in the upper right corner, click on "Edit".

![](/Deployment/images/10.png)


- Click on the "plus" in the section where you want to place the web part. 
- Type "perm" and click on the icon of the "Permission Center". 

![](/Deployment/images/11.png)

- Republish the page.

![](/Deployment/images/12.png)