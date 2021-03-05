---
title: "Permission Center web part"
date: 2021-03-01T14:38:53-06:00
draft: false
---
# Permission Center web part
Karsten Held, 10.02.2021

## Introduction

The &quot;SharePoint Permission Center web part&quot; is a modern SharePoint web part for SharePoint Online, released as open source under the [MIT License](https://choosealicense.com/licenses/mit/) by the company WhizzyApps GmbH.

[Sourcecode on GitHub](https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part)

The web part makes it easier for site owners and users to answer the following questions:

- Who has access to a site collection and with what permission level?
- What are the members of a SharePoint group including members of nested Azure groups?
- Why is a person member of a particular group?
- What is the group nesting hierarchy of SharePoint and Azure groups?
- What (hidden) groups do exist from shared documents and folders in the site?
- What other (hidden) groups do exist without any assigned permission level?
- How can I navigate to the classic SharePoint pages to manage groups and permissions?

![](/images/1%20Introduction.png)

It also gives site owners simple means to quickly change the group membership or users.

## Problem statement

With the introduction of a new type of Azure group - the &quot;Office 365 group&quot; (now called &quot;Microsoft 365 group&quot; or &quot;M365 group&quot;) - Microsoft changed the way we manage access to SharePoint sites. The M365 group allows the management of access to many apps in one single place:

- Microsoft Teams team
- SharePoint Online site
- Outlook mailbox
- Microsoft Planner plan
- Yammer community or group
- Microsoft Stream channel
- PowerBI workspace

To give members of an M365 group access to a SharePoint site collection, Microsoft decided to add the M365 group to the classic SharePoint site members group and make the owners of the M365 group site collection admins. This means the SharePoint site members group contains the M365 group which in turn contains the members. Many site owners - especially those who already have experience in using classic sites - are not of aware of this group nesting and have difficulties understanding the two parallel permission mechanisms that define the permissions of users in modern group-connected sites:

- The classic SharePoint groups which can contain both users and any type of Azure group
- The M365 group that controls who is a site member and who is site collection admin

Currently we see 3 commonly used types of SharePoint sites:

1. The modern team site that is connected to an M365 group (Template GROUP#0)
2. The modern communication site that is not connected to an M365 group (Template SITEPAGEPUBLISHING#0)
3. The classic team site that is not connected to an M365 group (Template STS#0)

The problem is that both navigation and management of permissions is different depending on the type of site.

<img src="/Images/2%20Problem%20Statment%201.png" style="width:auto;max-width:800"/>

In modern group-connected sites (left) the site settings page no longer contains &quot;People and groups&quot; and &quot;Site permissions&quot;.

<img src="/Images/3%20Problem%20Statment%202.png" style="width:auto;max-width:800"/>

In SharePoint sites without a group-connection (2. and 3.) you see the &quot;Share&quot; option on the top right of every page while in group-connected sites (1.) this is replaced by the &quot;Members&quot; option. The &quot;Members&quot; option will only show you the members of the M365 group. If other users have been added to classic SharePoint groups they will not show up here despite having access. Also in the M365 group the concept of the visitor is missing.

These design decisions cause a lot of misunderstandings. Users who expect a consistent and unified experience for managing access and permissions have trouble understanding the various implications of the different types of sites. They can either see the M365 group members or the SharePoint group members. There is no practical way to show both in one single view. Members of other types of nested Azure groups (security groups, mail-enabled security groups, distribution lists) cannot be shown at all. Also changing the group membership requires expert knowledge because the user experience is inconsistent:

- for SharePoint groups, go to gear icon \&gt; Site permissions \&gt; Advanced permission settings
- for the M365 group, go to &quot;Members&quot; on the top right of the site
- for other nested Azure groups, go to the Azure Portal \&gt; Active Directory \&gt; Groups

Another category of problem is that site owners cannot easily see what documents have been shared with whom. They have trouble reviewing all given accesses and removing those users who should not have access to the site anymore. Even experts are often not aware of the fact that each individual sharing of a document or folder creates a hidden group and breaks permission inheritance for that item.

The Permission Center web part solves these problems by providing a unified and exhaustive user interface to review and manage all users and groups that have access to a site. It also gives access to all classic SharePoint pages for permission management via the &quot;SharePoint&quot; menu.

## Deployment instructions

1) Download the web part package file _permission-center-webpart.sppkg_ from
[https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part/releases](https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part/releases)
Do not rename the file. The filename has to match the package name.

2) You can deploy the web part to either

**A) The SharePoint global app catalog site (as SharePoint admin).**
 If you do so, all your site collections will be able to use the web part.

**B) Or an existing site collection app catalog (as Site collection admin).**
 In this case the web part can only be used in this particular site collection and nowhere else. This is useful if you want to install a specific version of the web part for testing and verification.

### 2A) Deployment to the global app catalog

Navigate to your App Catalog site. If you don&#39;t know the URL of your App Catalog site, follow these steps:

Navigate to the SharePoint company app catalog go to the Microsoft 365 admin center \&gt; Show all \&gt; SharePoint \&gt; Sites \&gt; Active sites or use this link: https://[YOUR\_TENANT]-admin.sharepoint.com/\_layouts/15/online/AdminHome.aspx#/siteManagement/view/ALL%20SITES Then in the &quot;Template&quot; column filter by &quot;App Catalog Site&quot; and click on the App Catalog Site URL.

<img src="/Images/4 Deployment 1.png" style="width:auto;max-width:800"/>


Some tenants do not have

In the App Catalog Site click on &quot;Apps for SharePoint&quot; \&gt; New \&gt; Choose Files \&gt; select the downloaded _permission-center-webpart.sppkg_ file \&gt; OK \&gt; then click &quot;Deploy&quot;.

<img src="/Images/5 Deployment 2.png" style="width:auto;max-width:800"/>

After the deployment, make sure the file is checked in. If you see an icon with a small green arrow you need to manually check the file in: Click the ellipsis (...) icon of the file \&gt; ... \&gt; Advanced \&gt; Check In \&gt; OK

<img src="/Images/6 Deployment 3.png" style="width:auto;max-width:800"/>

### 2B) Deployment to a site collection app catalog

Navigate
