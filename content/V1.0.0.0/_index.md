---
title: "Version 1.0.0.0"
date: 2021-03-01T14:38:53-06:00
draft: false
weight: 99
---
Samuel Gross, 10.02.2021

### Web part Features

{{< rawhtml >}}
<div style="overflow-wrap: normal;">
{{</ rawhtml >}}

1. **Groups tab** 

      {{< figure src="/V1.0.0.0/images/Feature01.png" class="right300" >}}
      - Showing groups
        - "Site Admins" (not a particular SharePoint group)
        - Default site groups: "Site Owners", "Site Members", "Site Visitors"
        - Custom SharePoint groups: "Dolani special"
        - "Access given directly" (not a particular SharePoint group)
      - Showing permission levels in parentheses
        - For groups. To manage permissions of a particular permission level, click to open classic page
        - For each member with direct access
      - Expand/Collapse group members: click on icon on the left
      - Manage groups
        - Icons on the right with tooltip
        - For "Site Admins" and "Access given directly" open "classic permissions page"
        - For SharePoint groups expand group card. See section "Group card".
      - Manage users: Click on username to open user card. See section "User card".
      
2. **Users tab** 

      {{< figure src="/V1.0.0.0/images/Feature02.png" class="right300" >}}
      - Showing all users of site in Alphabetical order
      - Showing permission levels in parentheses
      - Manage users: Click on username to open user card. See section "User card".

3. **Hidden groups tab** 

      {{< figure src="/V1.0.0.0/images/Feature03.png" class="right300" >}}
      - Showing hidden SharePoint groups that are created by SharePoint and their members
      - "Limited Access System Group"
      - Sharing groups
        - Are created when an item is shared
        - Sharing: [Item name] [SharePoint group name]
        - Link to open item
        - Link to open classic permissions page of item
        - Showing permissions in parentheses
      - Manage groups: Click on edit icon on the right expands group card. See section "Group card".
      - Manage users: Click on username opens user card. See section "User card".

4. ***Group card*** 

      {{< figure src="/V1.0.0.0/images/Feature04.png" class="right300" >}}
      - Click on edit icon expands group card
      - Showing details
        - Name, Type
        - If it is set as a default group
        - Group owner
        - Permission levels
      - Action buttons
        - "Edit group" opens classic group settings page
        - "delete group" removes group from SharePoint
        - "Show group in SharePoint" opens classic group page
        - "Edit group permissions" opens classic permissions page of group
      

5. ***User Card***

      {{< figure src="/V1.0.0.0/images/Feature05.png" class="right300" >}}
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
        - "Change membership" opens dialog to add or remove the user to/from a group. See section "Change membership"
        - "Delete user from site" removes user from all SharePoint groups of the site and deletes its SharePoint profile
        - "Classic property page" opens classic user property page
      - Change membership
        {{< figure src="/V1.0.0.0/images/Feature06.png" class="right500" >}}
        - List of all Sharepoint groups of site, including hidden groups and "Access given directly"
        - List of all Azure groups of site, ordered by type: M365, Security, Distribution List, Mail-enabled Security
        - To add/remove user from groups, select/deselect group and click on button "Change membership"
        - To manage members of "Access given directly", click to open classic permission page
        - To manage members of Distribution List and Mail-enabled Security group, click to open group in Azure portal

6. **SharePoint menu** 
  
      {{< figure src="/V1.0.0.0/images/Feature07.png" class="right300" >}}
      - Access to 6 particular pages of classic admin center:
      - "Classic permissions page" opens "../user.aspx"
      - "Classic permissions level page" opens page of all permission levels of site
      - "Classic groups page" opens "../groups.aspx"
      - "Classic default groups page" opens "../permsetup.aspx"
      - "Classic all site users page" opens "../people.aspx?MembershipGroupId=0"
      - "Classic access request page" opens "../pendingreq.aspx"

7. **Reload button** 

      {{< figure src="/V1.0.0.0/images/Feature08.png" class="right300" >}}
      - Reloads webpart with updated data from the Api without reloading the web page

### Web part configuration 

  {{< figure src="/V1.0.0.0/images/Configuration01.png" class="right250" >}}

  To configure the webpart, edit page, then edit web part. The web part "property pane" will blend in on the right. 

**About the web part**

- Version number
- Build time stamp
- Link for documentation

Note: You need to be site owner or site admin to be able to configure the web part, otherwise no options will be shown.

**Configuration based on permissions**

- On (by default):
  - The web part checks the permission level of the current user based on typical permissions for the permission levels "Full control", "Edit" or "Read" and categorizes the user to be Owner, Member or Visitor.
  - Based on that, the web part is displayed with a particular configuration. You can decide, which features are shown for which permission.
  - Configure web part for "Site owners", "Site members" and "Site visitors" (Drop down menu)
  - Switch on/off the features listed below.
  - If you are Site owner, you will see the changes you make for the configuration of "Site owners" in the web part immediately.
  - If you are site admin, the web part will not reflect the changes, because for admins, all features are enabled.
  - By default, the typical features are enabled.

{{< rawhtml >}}
  <br style="clear:both;"/>
{{</ rawhtml >}}

- Off: 
  {{< figure src="/V1.0.0.0/images/Configuration02.png" class="right250clear" >}}
  - For all users you can switch on/off the features, despite their permissions. The same features are configurable as for the Configuration based on permissions is "On".
  - By default, all features are enabled.
  - Web part will reflect changes immediately.

- Security Note
  - For both ("Configuration based on permissions" enabled or disabled), features that are restricted by SharePoint for the current user, will not be shown or will be empty.
  - For example: Site members do not have permissions to see the site admins, so the site admins will not be shown in the web part, even if the feature "Show Site Admins" is enabled.
  - So the web part will only display information the user has access to based on the user permissions controlled through SharePoint itself.

### Special behaviors: Hidden groups

Groups that either have no permissions or just have the permission level "Limited Access" are considered in the web part as a hidden group.

Examples of hidden groups: 
  {{< figure src="/V1.0.0.0/images/Special01.png" class="right300" >}}

  - **Custom groups without assigned permission level:** See picture group 1. You can create a SharePoint group without assigning it any permission level.
  - **SharePoint built-in groups without assigned permission level:** See picture group 2. There are groups, created by SharePoint, that don't have any permission level or the permission level "Limited Access".
  - **Active sharing links:** See picture group 3. If you share an item (document, folder, page), a SharePoint group is created. Since it doesn't have a site permission level, it is a hidden group. The permission level shown in parentheses is on item level. If the sharing link is active, the group is assigned to the item. The web part shows information about the item like the name "Document1" and in the tooltip the link type.
  - **Inactive sharing links:** See picture group 4. If the sharing link is broken or the item is deleted, the group still exists, but it is not assigned to an item. The web part shows just the name of the SharePoint group. This is explained below.
  - **Limited Access System group** : See picture group 5. The Limited Access permission is assigned to a user automatically by SharePoint when you give permission to the user to access a specific content item. But the user does not have permission to open or edit any other items in the library. You cannot assign this permission level to users or SharePoint groups.

#### Information about Sharing groups 
  {{< figure src="/V1.0.0.0/images/Special02.png" class="right250" >}}

If you share an item in a SharePoint list, you have 4 options how to share the item:

- Anyone with the link
- People in your Organization with the link
- People with existing access
- Specific people

You can choose if user can read or edit the item.

**Anyone with the link**

This option needs to be enabled in the Admin center. The name of the created group contains "Anonymous", because anyone can access the item, and "View" for the read permission.

  {{< figure src="/V1.0.0.0/images/Special03.png" class="left600" >}}


**People in your Organization with the link**

The name of the created group contains "Organization", because only people in your organization can access the item, and "Edit" for the edit permission.

  {{< figure src="/V1.0.0.0/images/Special04.png" class="left600" >}}

**People with existing access**

This option is just to send a link to specified user. No SharePoint group is created.

**Specific people**

With this option, only invited people can access the item. The name of the created group contains "Flexible", because you can change the permissions of this group to edit or read.

  {{< figure src="/V1.0.0.0/images/Special05.png" class="left600" >}}

{{< rawhtml >}}
</div>
{{</ rawhtml >}}

### Where does the data come from?

#### SharePoint API endpoints:

Get current user permissions

- `{site url}/\_api/web/currentuser/isSiteAdmin`
- `{site url}/\_api/web/effectiveBasePermissions`

Get default site groups:

- `{site url}/\_api/web/AssociatedOwnerGroup`
- `{site url}/\_api/web/AssociatedMemberGroup`
- `{site url}/\_api/web/AssociatedVisitorGroup`

Get all site groups:

- `{site url}/\_api/web/sitegroups`

Get members with access given directly:

- `{site url} /\_api/web/RoleAssignments? $expand=Member,RoleDefinitionBindings&amp;$filter=Member/PrincipalType ne 8`

Get site admins:

- `{site url}/\_api/web/siteusers?$filter=IsSiteAdmin eq true`

Get group permissions:

- `{site url}/\_api/Web/RoleAssignments/GetByPrincipalId({group id})/RoleDefinitionBindings`

Get group members:

- `{site url}/\_api/web/SiteGroups/GetById({group id})/users`

Get all site permission levels:

- `{site url}/\_api/web/roleDefinitions`

Get properties of sharing groups:

- `{site url}/\_api/search/query?querytext='{guid}'`

Get properties of sharing groups in case of link type "specific people"

- `{site url} /\_api/web/Lists('{listId}')/GetItemByUniqueId('{guid}')/GetSharingInformation? $Expand=permissionsInformation`

Get all groups, that have permission levels:

- `{site url}/\_api/Web/RoleAssignments`

Delete group

- `{site url}/\_api/web/sitegroups/removebyid({group id})`

Delete sharing group

- `{site url}/\_api/web/Lists('{listId}')/GetItemByUniqueId('{itemId}')/UnshareLink`

Get id of shared item to open permissions page of item

- `{site url}/\_api/web/Lists('{listId}')/GetItemByUniqueId('{guid}')`

Add/ remove user to/from admins: post user with attribute "isSiteAdmin" = true/false

- `{site url}/\_api/web/GetUserById({userId})`
- In case SharePoint id not available: Get SharePoint id of user
  - `{site url}/\_api/web/siteusers(@v)?@v='{userLoginName}'`
- To add: in case user has no profile in SharePoint: create profile via post
  - `{site url}/\_api/web/ensureuser`

Add user to group: post with body 'loginName': userLoginName

- `{site url}/\_api/web/sitegroups/getbyid({groupId})/users`

Remove user from group: post with body 'loginName': userLoginName

- `{site url}/removeByLoginName`

Delete user from site: post with header: 'X-HTTP-Method': 'DELETE'

- `{site url}/\_api/web/GetUserById({userSpId})`

#### Graph API endpoints:

Get members of Azure groups:

- `/groups/{azureGroupId}/members`

Get owners of Azure groups:

- `/groups/{azureGroupId}/owners`

Get properties of Azure groups:

- `/groups/{azureGroupId}`

Get name of organization of tenant to display it in tooltip for sharing groups

- `/organization`

Get azure properties for user

- `/users/{userPrincipalName}`
