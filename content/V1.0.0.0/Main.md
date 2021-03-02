---
title: "Documentation for PermissionCenter web part version 1.0.0.0"
date: 2021-03-01T14:38:53-06:00
draft: false
---

# SharePoint Permission Center Web Part

Version 1.0.0.0

Karsten Held, 2020-12-30

# Introduction

The &quot;SharePoint Permission Center web part&quot; is a modern SharePoint web part for SharePoint Online, released as open source under the [MIT License](https://choosealicense.com/licenses/mit/) by the company WhizzyApps GmbH.

Sourcecode on GitHub: [https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part](https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part)
 Documentation: [https://sharepoint-permission-center.com/](https://sharepoint-permission-center.com/)

The web part makes it easier for site owners and users to answer the following questions:

- Who has access to a site collection and with what permission level?
- What are the members of a SharePoint group including members of nested Azure groups?
- Why is a person member of a particular group?
- What is the group nesting hierarchy of SharePoint and Azure groups?
- What (hidden) groups do exist from shared documents and folders in the site?
- What other (hidden) groups do exist without any assigned permission level?
- How can I navigate to the classic SharePoint pages to manage groups and permissions?

![](/V1.0.0.0/Images/1%20Introduction.png)

It also gives site owners simple means to quickly change the group membership or users.

# Problem statement

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

<img src="/V1.0.0.0/Images/2%20Problem%20Statment%201.png" style="width:auto;max-width:800"/>

In modern group-connected sites (left) the site settings page no longer contains &quot;People and groups&quot; and &quot;Site permissions&quot;.

<img src="/V1.0.0.0/Images/3%20Problem%20Statment%202.png" style="width:auto;max-width:800"/>

In SharePoint sites without a group-connection (2. and 3.) you see the &quot;Share&quot; option on the top right of every page while in group-connected sites (1.) this is replaced by the &quot;Members&quot; option. The &quot;Members&quot; option will only show you the members of the M365 group. If other users have been added to classic SharePoint groups they will not show up here despite having access. Also in the M365 group the concept of the visitor is missing.

These design decisions cause a lot of misunderstandings. Users who expect a consistent and unified experience for managing access and permissions have trouble understanding the various implications of the different types of sites. They can either see the M365 group members or the SharePoint group members. There is no practical way to show both in one single view. Members of other types of nested Azure groups (security groups, mail-enabled security groups, distribution lists) cannot be shown at all. Also changing the group membership requires expert knowledge because the user experience is inconsistent:

- for SharePoint groups, go to gear icon \&gt; Site permissions \&gt; Advanced permission settings
- for the M365 group, go to &quot;Members&quot; on the top right of the site
- for other nested Azure groups, go to the Azure Portal \&gt; Active Directory \&gt; Groups

Another category of problem is that site owners cannot easily see what documents have been shared with whom. They have trouble reviewing all given accesses and removing those users who should not have access to the site anymore. Even experts are often not aware of the fact that each individual sharing of a document or folder creates a hidden group and breaks permission inheritance for that item.

The Permission Center web part solves these problems by providing a unified and exhaustive user interface to review and manage all users and groups that have access to a site. It also gives access to all classic SharePoint pages for permission management via the &quot;SharePoint&quot; menu.

# Deployment instructions

1) Download the web part package file _permission-center-webpart.sppkg_ from
[https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part/releases](https://github.com/WhizzyApps/SPO-Permission-Center-Web-Part/releases)
Do not rename the file. The filename has to match the package name.

2) You can deploy the web part to either

**A) The SharePoint global app catalog site (as SharePoint admin).**
 If you do so, all your site collections will be able to use the web part.

**B) Or an existing site collection app catalog (as Site collection admin).**
 In this case the web part can only be used in this particular site collection and nowhere else. This is useful if you want to install a specific version of the web part for testing and verification.

## 2A) Deployment to the global app catalog

Navigate to your App Catalog site. If you don&#39;t know the URL of your App Catalog site, follow these steps:

Navigate to the SharePoint company app catalog go to the Microsoft 365 admin center \&gt; Show all \&gt; SharePoint \&gt; Sites \&gt; Active sites or use this link: https://[YOUR\_TENANT]-admin.sharepoint.com/\_layouts/15/online/AdminHome.aspx#/siteManagement/view/ALL%20SITES Then in the &quot;Template&quot; column filter by &quot;App Catalog Site&quot; and click on the App Catalog Site URL.

<img src="/V1.0.0.0/Images/4 Deployment 1.png" style="width:auto;max-width:800"/>


Some tenants do not have

In the App Catalog Site click on &quot;Apps for SharePoint&quot; \&gt; New \&gt; Choose Files \&gt; select the downloaded _permission-center-webpart.sppkg_ file \&gt; OK \&gt; then click &quot;Deploy&quot;.

<img src="/V1.0.0.0/Images/5 Deployment 2.png" style="width:auto;max-width:800"/>

After the deployment, make sure the file is checked in. If you see an icon with a small green arrow you need to manually check the file in: Click the ellipsis (…) icon of the file \&gt; … \&gt; Advanced \&gt; Check In \&gt; OK

<img src="/V1.0.0.0/Images/6 Deployment 3.png" style="width:auto;max-width:800"/>

**2B) Deployment to a site collection app catalog**

Navigate

# Web part description

Features

1. &quot; **Groups&quot; tab** <img src="/V1.0.0.0/Images/7 Description 1.png" style="width:300; float:right"/>

- Showing groups
  - &quot;Site Admins&quot; (not a particular SharePoint group)
  - default site groups: &quot;Site Owners&quot;, &quot;Site Members&quot;, &quot;Site Visitors&quot;
  - custom SharePoint groups: &quot;Dolani special&quot;
  - &quot;Access given directly&quot; (not a particular SharePoint group)
- Showing permission levels in brackets
  - f groups. To manage permissions of a particular permission level, click to open classic page
  - f each member with direct access
- Expand/Collapse group members: click on icon on the left
- Manage groups:
  - Icons on the right with tooltip
  - For &quot;Site Admins&quot; and &quot;Access given directly&quot; open &quot;classic permissions page&quot;
  - For SharePoint groups expand group card. See section &quot;Group card&quot;.
- Manage users: Click on username to open user card. See section &quot;User card&quot;.

1. ![](RackMultipart20210301-4-y1hube_html_c41fd0d5e0fa4159.png)&quot; **Users&quot; tab**

- Showing all users of site in Alphabetical order
- Showing permission levels in brackets
- Manage users: Click on username to open user card. See section &quot;User card&quot;.

1. ![](RackMultipart20210301-4-y1hube_html_6a654d018b5b1dca.png)&quot; **Hidden groups&quot; tab**

- Showing hidden SharePoint groups that are created by SharePoint and their members
- &quot;Limited Access System Group&quot;
- Sharing groups
  - are created when an item is shared
  - Sharing: \&lt;Item name\&gt; \&lt;SharePoint group name\&gt;
  - Link to open item
  - Link to open classic permissions page of item
  - Showing permissions in brackets
- Manage groups: Click on edit icon on the right expands group card. See section &quot;Group card&quot;.
- Manage users: Click on username opens user card. See section &quot;User card&quot;.

1. ![](RackMultipart20210301-4-y1hube_html_aa57eb840486a6c.png) **Group card**

- Click on edit icon expands group card
- Showing details
  - Name, Type
  - If it is set as a default group
  - Group owner
  - Permission levels
- Action buttons
  - &quot;Edit group&quot; opens classic group settings page
  - &quot;delete group&quot; removes group from SharePoint
  - &quot;Show group in SharePoint&quot; opens classic group page
  - &quot;Edit group permissions&quot; opens classic permissions page of group

1. ![](RackMultipart20210301-4-y1hube_html_509446fad43b71b1.png) **User Card**

- Click on username opens user card.
- Showing details
  - User photo
  - Email address
  - Permission levels
- Membership in all groups
  - SharePoint group and permission level: Click opens classic group page
  - Nested Azure groups (Type, name): Click opens group in Azure portal
  - Username: Click opens user in Azure portal
- Action buttons:
  - &quot;Change membership&quot; opens dialog to add or remove the user to/from a group. See section &quot;Change membership&quot;
  - &quot;Delete user from site&quot; removes user from all SharePoint groups of the site and deletes its SharePoint profile
  - &quot;Classic property page&quot; opens classic user property page
- ![](RackMultipart20210301-4-y1hube_html_90ea1bcb997f57b.png)Change membership
  - List of all Sharepoint groups of site, including hidden groups and &quot;Access given directly&quot;
  - List of all Azure groups of site, ordered by type: M365, Security, Distribution List, Mail-enabled Security
  - To add/remove user from groups, select/deselect group and click on button &quot;Change membership&quot;
  - To manage members of &quot;Access given directly&quot;, click to open classic permission page
  - To manage members of Distribution List and Mail-enabled Security group, click to open group in Azure portal

1. ![](RackMultipart20210301-4-y1hube_html_c4c3962d4ba5636d.png) **SharePoint menu**

- Access to 6 particular pages of classic admin center:
- &quot;Classic permissions page&quot; opens &quot;../user.aspx&quot;
- &quot;Classic permissions level page&quot; opens page of all permission levels of site
- &quot;Classic groups page&quot; opens &quot;../groups.aspx&quot;
- &quot;Classic default groups page&quot; opens &quot;../permsetup.aspx&quot;
- &quot;Classic all site users page&quot; opens &quot;../people.aspx?MembershipGroupId=0&quot;
- &quot;Classic access request page&quot; opens &quot;../pendingreq.aspx&quot;

1. ![](RackMultipart20210301-4-y1hube_html_12292a50f860897.png) **Reload button**

- Reloads webpart with updated data from the Api without reloading the web page

# ![](RackMultipart20210301-4-y1hube_html_9087c981625b89d2.png)Web part configuration

To configure the webpart, edit page, then edit web part. The web part &quot;property pane&quot; will blend in on the right.

About the web part

- Version number
- Build time stamp
- Link for documentation

Note: You need to be site owner or site admin to be able to configure the web part, otherwise no options will be shown.

Configuration based on permissions

- On (by default):
  - The web part checks the permission level of the current user based on typical permissions for the permission levels &quot;Full control&quot;, &quot;Edit&quot; or &quot;Read&quot; and categorizes the user to be Owner, Member or Visitor.
  - Based on that, the web part is displayed with a particular configuration. You can decide, which features are shown for which permission.
  - Configure web part for &quot;Site owners&quot;, &quot;Site members&quot; and &quot;Site visitors&quot; (Drop down menu)
  - Switch on/off the features listed below.
  - If you are Site owner, you will see the changes you make for the configuration of &quot;Site owners&quot; in the web part immediately.
  - If you are site admin, the web part will not reflect the changes, because for admins, all features are enabled.
  - By default, the typical features are enabled.

- ![](RackMultipart20210301-4-y1hube_html_5317bf147ad6bfc9.png)Off:
  - For all users you can switch on/off the features, despite their permissions. The same features are configurable as for the Configuration based on permissions is &quot;On&quot;.
  - By default, all features are enabled.
  - Web part will reflect changes immediately.

- Security Note
  - For both (&quot;Configuration based on permissions&quot; enabled or disabled), features that are restricted by SharePoint for the current user, will not be shown or will be empty.
  - For example: Site members do not have permissions to see the site admins, so the site admins will not be shown in the web part, even if the feature &quot;Show Site Admins&quot; is enabled.
  - So the web part will only display information the user has access to based on the user permissions controlled through SharePoint itself.

Special behaviors: Hidden groups

Groups that either have no permissions or just have the permission level &quot;Limited Access&quot; are considered in the web part as a hidden group.

![](RackMultipart20210301-4-y1hube_html_7be3da80f9074d9e.png)Examples of hidden groups:

- **Custom groups without assigned permission level:** See picture group 1. You can create a SharePoint group without assigning it any permission level.
- **SharePoint built-in groups without assigned permission level:** See picture group 2. There are groups, created by SharePoint, that don&#39;t have any permission level or the permission level &quot;Limited Access&quot;.
- **Active sharing links:** See picture group 3. If you share an item (document, folder, page), a SharePoint group is created. Since it doesn&#39;t have a site permission level, it is a hidden group. The permission level shown in brackets is on item level. If the sharing link is active, the group is assigned to the item. The web part shows information about the item like the name &quot;Document1&quot; and in the tooltip the link type.
- **Inactive sharing links:** See picture group 4. If the sharing link is broken or the item is deleted, the group still exists, but it is not assigned to an item. The web part shows just the name of the SharePoint group. This is explained below.
- **Limited Access System group** : See picture group 5. The Limited Access permission is assigned to a user automatically by SharePoint when you give permission to the user to access a specific content item. But the user does not have permission to open or edit any other items in the library. You cannot assign this permission level to users or SharePoint groups.

![](RackMultipart20210301-4-y1hube_html_86a4b8be4a72bcf5.png)Information about Sharing groups

If you share an item in a SharePoint list, you have 4 options how to share the item:

- Anyone with the link
- People in your Organization with the link
- People with existing access
- Specific people

You can choose if user can read or edit the item.

**Anyone with the link**

This option needs to be enabled in the Admin center. The name of the created group contains &quot;Anonymous&quot;, because anyone can access the item, and &quot;Edit&quot; for the edit permission.

![](RackMultipart20210301-4-y1hube_html_69c163c3787e55e5.png)

**People in your Organization with the link**

The name of the created group contains &quot;Organization&quot;, because only people in your organization can access the item, and &quot;view&quot; for the read permission.

![](RackMultipart20210301-4-y1hube_html_e19f046281514a7b.png)

**People with existing access**

This option is just to send a link to specified user. No SharePoint group is created.

**Specific people**

With this option, only invited people can access the item. The name of the created group contains &quot;Flexible&quot;, because you can change the permissions of this group to view or read.

![](RackMultipart20210301-4-y1hube_html_4cc7975dcd35989c.png)

Where does the data come from?

SharePoint API endpoints:

Get current user permissions

- {site url}/\_api/web/currentuser/isSiteAdmin
- {site url}/\_api/web/effectiveBasePermissions

Get default site groups:

- {site url}/\_api/web/AssociatedOwnerGroup
- {site url}/\_api/web/AssociatedMemberGroup
- {site url}/\_api/web/AssociatedVisitorGroup

Get all site groups:

- {site url}/\_api/web/sitegroups

Get members with access given directly:

- {site url} /\_api/web/RoleAssignments? $expand=Member,RoleDefinitionBindings&amp;$filter=Member/PrincipalType ne 8

Get site admins:

- {site url}/\_api/web/siteusers?$filter=IsSiteAdmin eq true

Get group permissions:

- {site url}/\_api/Web/RoleAssignments/GetByPrincipalId({group id})/RoleDefinitionBindings

Get group members:

- {site url}/\_api/web/SiteGroups/GetById({group id})/users

Get all site permission levels:

- {site url}/\_api/web/roleDefinitions

Get properties of sharing groups:

- {site url}/\_api/search/query?querytext=&#39;{guid}&#39;

Get properties of sharing groups in case of link type &quot;specific people&quot;

- {site url} /\_api/web/Lists(&#39;{listId}&#39;)/GetItemByUniqueId(&#39;{guid}&#39;)/GetSharingInformation? $Expand=permissionsInformation

Get all groups, that have permission levels:

- {site url}/\_api/Web/RoleAssignments

Delete group

- {site url}/\_api/web/sitegroups/removebyid({group id})

Delete sharing group

- {site url}/\_api/web/Lists(&#39;{listId}&#39;)/GetItemByUniqueId(&#39;{itemId}&#39;)/UnshareLink

Get id of shared item to open permissions page of item

- {site url}/\_api/web/Lists(&#39;{listId}&#39;)/GetItemByUniqueId(&#39;{guid}&#39;)

Add/ remove user to/from admins: post user with attribute &quot;isSiteAdmin&quot; = true/false

- {site url}/\_api/web/GetUserById({userId})
- In case SharePoint id not available: Get SharePoint id of user
  - {site url}/\_api/web/siteusers(@v)?@v=&#39;{userLoginName}&#39;
- To add: in case user has no profile in SharePoint: create profile via post
  - {site url}/\_api/web/ensureuser

Add user to group: post with body &#39;loginName&#39;: userLoginName

- {site url}/\_api/web/sitegroups/getbyid({groupId})/users

Remove user from group: post with body &#39;loginName&#39;: userLoginName

- {site url}/removeByLoginName

Delete user from site: post with header: &#39;X-HTTP-Method&#39;: &#39;DELETE&#39;

- {site url}/\_api/web/GetUserById({userSpId})

Graph API endpoints:

Get members of Azure groups:

- /groups/{azureGroupId}/members

Get owners of Azure groups:

- /groups/{azureGroupId}/owners

Get properties of Azure groups:

- /groups/{azureGroupId}

Get name of organization of tenant to display it in tooltip for sharing groups

- /organization

Get azure properties for user

- /users/{userPrincipalName}

![](RackMultipart20210301-4-y1hube_html_6a354e01d9b36d34.gif)

Confidentiality: C2 - Internal