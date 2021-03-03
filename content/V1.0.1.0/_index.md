---
title: "Version 1.0.1.0"
date: 2021-03-01T14:39:08-06:00
draft: false
---
Samuel Gross, 04.03.2021

## Release notes

- All SharePoint system groups are now shown in the web part. For example: SharePoint Administrator&quot;, SharePoint Service Administrator&quot;, Company Administrator&quot;, &quot;Everyone Except external users&quot;. They are listed as a user and can be managed via user card: &quot;change membership&quot; and &quot;delete user from site&quot;.
- Usernames are sorted not just as a string:
  - mutated vowel: ö is treated as o, etc.
  - numbers as numbers: 2 before 10
- SharePoint Api call to get members of azure groups: get 500 users per request, instead of 1000.
- User card expands without animation by default. Switch it on in debug mode.

## Web part description

### Features

1. ![](RackMultipart20210302-4-skngrt_html_286f05ecb30db67f.png)&quot; **Groups&quot; tab**

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

1. ![](RackMultipart20210302-4-skngrt_html_c41fd0d5e0fa4159.png)&quot; **Users&quot; tab**

- Showing all users of site in Alphabetical order
- Showing permission levels in brackets
- Manage users: Click on username to open user card. See section &quot;User card&quot;.

1. ![](RackMultipart20210302-4-skngrt_html_6a654d018b5b1dca.png)&quot; **Hidden groups&quot; tab**

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

1. ![](RackMultipart20210302-4-skngrt_html_aa57eb840486a6c.png) **Group card**

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

1. ![](RackMultipart20210302-4-skngrt_html_509446fad43b71b1.png) **User Card**

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
- ![](RackMultipart20210302-4-skngrt_html_90ea1bcb997f57b.png)Change membership
  - List of all Sharepoint groups of site, including hidden groups and &quot;Access given directly&quot;
  - List of all Azure groups of site, ordered by type: M365, Security, Distribution List, Mail-enabled Security
  - To add/remove user from groups, select/deselect group and click on button &quot;Change membership&quot;
  - To manage members of &quot;Access given directly&quot;, click to open classic permission page
  - To manage members of Distribution List and Mail-enabled Security group, click to open group in Azure portal

1. ![](RackMultipart20210302-4-skngrt_html_c4c3962d4ba5636d.png) **SharePoint menu**

- Access to 6 particular pages of classic admin center:
- &quot;Classic permissions page&quot; opens &quot;../user.aspx&quot;
- &quot;Classic permissions level page&quot; opens page of all permission levels of site
- &quot;Classic groups page&quot; opens &quot;../groups.aspx&quot;
- &quot;Classic default groups page&quot; opens &quot;../permsetup.aspx&quot;
- &quot;Classic all site users page&quot; opens &quot;../people.aspx?MembershipGroupId=0&quot;
- &quot;Classic access request page&quot; opens &quot;../pendingreq.aspx&quot;

1. ![](RackMultipart20210302-4-skngrt_html_12292a50f860897.png) **Reload button**

- Reloads webpart with updated data from the Api without reloading the web page

# ![](RackMultipart20210302-4-skngrt_html_d0e071861169c73b.png)Web part configuration

Configuration page 1/2

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

- ![](RackMultipart20210302-4-skngrt_html_5317bf147ad6bfc9.png)Off:
  - For all users you can switch on/off the features, despite their permissions. The same features are configurable as for the Configuration based on permissions is &quot;On&quot;.
  - By default, all features are enabled.
  - Web part will reflect changes immediately.

- Security Note
  - For both (&quot;Configuration based on permissions&quot; enabled or disabled), features that are restricted by SharePoint for the current user, will not be shown or will be empty.
  - For example: Site members do not have permissions to see the site admins, so the site admins will not be shown in the web part, even if the feature &quot;Show Site Admins&quot; is enabled.
  - So the web part will only display information the user has access to based on the user permissions controlled through SharePoint itself.

![](RackMultipart20210302-4-skngrt_html_a8de5fe4d09fe54c.png)Configuration page 2/2

The debug page is for developers to log the following to the developer console in case of bugs. By default it is switched off.

- Log state: react has a variable called &quot;state&quot;. When the web part has finished loading, the last state will be logged.
- Throw errors: by default all errors are catched. Enabled it to rethrow them.
- Log errors. By default all errors are catched and not logged. Enable it to log them to the console.
- Log variables of PermissionCenter.tsx: This is the main react component in the source code. If enabled, the most important variables of most functions are logged.
- Log variables of other components: Enable to log most important variables of most functions of all other react components.
- Use animate height for user card: Sometimes the user card doesn&#39;t expand. Disable it to try to expand it without animation.

Special behaviors: Hidden groups

Groups that either have no permissions or just have the permission level &quot;Limited Access&quot; are considered in the web part as a hidden group.

![](RackMultipart20210302-4-skngrt_html_7be3da80f9074d9e.png)Examples of hidden groups:

- **Custom groups without assigned permission level:** See picture group 1. You can create a SharePoint group without assigning it any permission level.
- **SharePoint built-in groups without assigned permission level:** See picture group 2. There are groups, created by SharePoint, that don&#39;t have any permission level or the permission level &quot;Limited Access&quot;.
- **Active sharing links:** See picture group 3. If you share an item (document, folder, page), a SharePoint group is created. Since it doesn&#39;t have a site permission level, it is a hidden group. The permission level shown in brackets is on item level. If the sharing link is active, the group is assigned to the item. The web part shows information about the item like the name &quot;Document1&quot; and in the tooltip the link type.
- **Inactive sharing links:** See picture group 4. If the sharing link is broken or the item is deleted, the group still exists, but it is not assigned to an item. The web part shows just the name of the SharePoint group. This is explained below.
- **Limited Access System group** : See picture group 5. The Limited Access permission is assigned to a user automatically by SharePoint when you give permission to the user to access a specific content item. But the user does not have permission to open or edit any other items in the library. You cannot assign this permission level to users or SharePoint groups.

![](RackMultipart20210302-4-skngrt_html_86a4b8be4a72bcf5.png)Information about Sharing groups

If you share an item in a SharePoint list, you have 4 options how to share the item:

- Anyone with the link
- People in your Organization with the link
- People with existing access
- Specific people

You can choose if user can read or edit the item.

**Anyone with the link**

This option needs to be enabled in the Admin center. The name of the created group contains &quot;Anonymous&quot;, because anyone can access the item, and &quot;Edit&quot; for the edit permission.

![](RackMultipart20210302-4-skngrt_html_69c163c3787e55e5.png)

**People in your Organization with the link**

The name of the created group contains &quot;Organization&quot;, because only people in your organization can access the item, and &quot;view&quot; for the read permission.

![](RackMultipart20210302-4-skngrt_html_e19f046281514a7b.png)

**People with existing access**

This option is just to send a link to specified user. No SharePoint group is created.

**Specific people**

With this option, only invited people can access the item. The name of the created group contains &quot;Flexible&quot;, because you can change the permissions of this group to view or read.

![](RackMultipart20210302-4-skngrt_html_4cc7975dcd35989c.png)

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

![](RackMultipart20210302-4-skngrt_html_6a354e01d9b36d34.gif)

Confidentiality: C2 - Internal