---
title: "Version 1.1.0"
date: 2021-12-01
draft: false
weight: 96
---
Karsten Held, Samuel Gross, 01.12.2021

### Release notes
- Bugfixes: 
  - A user was appearing twice in the "Groups" tab, because its prinzipal name in API responses was sometimes with upper case.
  - Show "Limited Access System Group For Web" under hidden groups. Because of "Limited Access System Group" got updated by Microsoft, now exist 2 different groups: "Limited Access System Group For List" and "Limited Access System Group For Web".
  - M365 group is incorrectly shown as user instead of being resolved.
  - When "Use animate height" off: Click on any button of user card incorrectly closes user card instead of staying expanded.
  - Sharing groups: “Open Item” did not open documents properly.
  - Users tab: If current user has no access to view permissions of SharePoint groups, after user name there was shown empty parenthesis instead of nothing.
- New features for debug mode:
  - Record API response. For debugging of a clients bug, replicate the clients API responses. Record them and download as a JSON file.
  - Preload Azure groups: possibility to reduce web part loading time by preloading Azure groups.
- Performance improved: Less graph API calls
  - Calls for getting Azure group type reduced by getting first 100 Azure groups of tenant at one call.
  - Web part configuration: If “Show Site Admins” or “Show Access given directly” = Off, don’t make API call.


### Web part features

{{< rawhtml >}}
<div style="overflow-wrap: normal;">
{{</ rawhtml >}}

1. **Groups tab** 

      {{< figure src="/V1.1.0/images/Feature01.png" class="right300" >}}
      - Showing groups
        - "Site Admins" (not a SharePoint group)
        - Default site groups: "Site Owners", "Site Members", "Site Visitors"
        - Custom SharePoint groups: "Dolani special"
        - "Access given directly" (not a SharePoint group)
      - Showing permission levels in parentheses
        - For groups. To manage permissions of a permission level, click to open classic page
        - For each member with direct access
      - Expand/Collapse group members: click on icon on the left
      - Manage groups
        - Icons on the right with tooltip
        - For "Site Admins" and "Access given directly" open "classic permissions page"
        - For SharePoint groups expand group card. See section "Group card".
      - Manage users: Click on username to open user card. See section "User card".
      
2. **Users tab** 

      {{< figure src="/V1.1.0/images/Feature02.png" class="right300" >}}
      - Showing all users of site in alphabetical order
      - Showing permission levels in parentheses
      - Manage users: Click on username to open user card. See section "User card".

3. **Hidden groups tab** 

      {{< figure src="/V1.1.0/images/Feature03.png" class="right300" >}}
      - Showing hidden SharePoint groups that are used by SharePoint and created by individual sharing.
      - "Limited Access System Group"
        - Contains all users who only have access to specific items of the site without being member of a SharePoint group
        - Used by individual sharing, e.g. if you share folders / files / list items using the "Share" function
        - Allows these users to browse to the item that was shared with them without seeing other items
        - Also contains users who had access to a specific item previously and where the access was removed
      - Sharing groups
        - Are created when an item is shared
        - Sharing: [Item name] [SharePoint group name]
        - Link to open item
        - Link to open classic permissions page of item
        - Showing permissions in parentheses
      - Manage groups: Click on edit icon on the right expands group card. See section "Group card".
      - Manage users: Click on username opens user card. See section "User card".

4. ***Group card*** 

      {{< figure src="/V1.1.0/images/Feature04.png" class="right300" >}}
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

      {{< figure src="/V1.1.0/images/Feature05.png" class="right300" >}}
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
        {{< figure src="/V1.1.0/images/Feature06.png" class="right500" >}}
        - List of all Sharepoint groups of site, including hidden groups and "Access given directly"
        - List of all Azure groups of site, ordered by type: M365, Security, Distribution List, Mail-enabled Security
        - To add/remove user from groups, select/deselect group and click on button "Change membership"
        - To change "Access given directly", click to open classic permission page
        - To manage memberships of Distribution lists and Mail-enabled security groups, click the group to open it in the Azure portal

6. **SharePoint menu** 
  
      {{< figure src="/V1.1.0/images/Feature07.png" class="right300" >}}
      - Access to SharePoint classic site administration pages:
      - "Classic permissions page" opens "[SITE_URL]/_layouts/15/user.aspx"
      - "Classic permissions level page" opens page of all permission levels of site
      - "Classic groups page" opens "[SITE_URL]/_layouts/15/groups.aspx"
      - "Classic default groups page" opens "[SITE_URL]/_layouts/15/permsetup.aspx"
      - "Classic all site users page" opens "[SITE_URL]/_layouts/15/people.aspx?MembershipGroupId=0"
      - "Classic access request page" opens "[SITE_URL]/_layouts/15/pendingreq.aspx"

7. **Reload button** 

      {{< figure src="/V1.1.0/images/Feature08.png" class="right300" >}}
      - Reloads webpart with updated data from the API without reloading the web page

### Web part configuration 

#### Configuration page 1

  {{< figure src="/V1.1.0/images/Configuration01.png" class="right250" >}}

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
  {{< figure src="/V1.1.0/images/Configuration02.png" class="right250clear" >}}
  - For all users you can switch on/off the features, despite their permissions. The same features are configurable as for the Configuration based on permissions is "On".
  - By default, all features are enabled.
  - Web part will reflect changes immediately.

- Security Note
  - For both ("Configuration based on permissions" enabled or disabled), features that are restricted by SharePoint for the current user, will not be shown or will be empty.
  - For example: Site members do not have permissions to see the site admins, so the site admins will not be shown in the web part, even if the feature "Show Site Admins" is enabled.
  - So the web part will only display information the user has access to based on the user permissions controlled through SharePoint itself.

#### Configuration page 2

{{< figure src="/V1.1.0/images/Configuration03.png" class="right250" >}}

The debug page is for developers to log the following to the developer console in case of bugs. By default it is switched off.

- Log state: react has a variable called "state". When the web part has finished loading, the last state will be logged.
- Throw errors: by default all errors are catched. Enabled it to rethrow them.
- Log errors. By default all errors are catched and not logged. Enable it to log them to the console.
- Log variables of PermissionCenter.tsx: This is the main react component in the source code. If enabled, the most important variables of most functions are logged.
- Log variables of other components: Enable to log most important variables of most functions of all other react components.
- Use animate height for user card: Sometimes the user card doesn't expand. Disable it to try to expand it without animation.
- Preload Azure groups
  - Improve performance for sites which contain many nested Azure groups. 
  - To identify if a group member is whether an Azure group or a user, for each member will be done an extra API call. 
  - To avoid those, the tenant Azure groups can be preloaded with only one call.
  - Default is on, because most sites have more than one nested Azure groups.
- Preload Azure groups amount 100 / 1000
  - Switch between maximum 100 and 1000 Azure groups.

{{< rawhtml >}}
  <br style="clear:both;"/>
{{</ rawhtml >}}

  {{< figure src="/V1.1.0/images/Configuration04.png" class="right250" >}}
  
- Export or import API response: For debugging of a clients bug, replicate the clients API responses. Record them and download as a JSON file.

### Special behaviors: Hidden groups

Groups that either have no permissions or just have the permission level "Limited Access" are considered in the web part as a hidden group.

Examples of hidden groups: 
  {{< figure src="/V1.1.0/images/Special01.png" class="right300" >}}

  1. **Custom groups without assigned permission level:** See picture group 1. You can create a SharePoint group without assigning it any permission level.
  2. **SharePoint built-in groups without assigned permission level:** See picture group 2. There are groups, created by SharePoint, that don't have any permission level or the permission level "Limited Access".
  3. **Active sharing links:** See picture group 3. If you share an item (document, folder, page), a SharePoint group is created. Since it doesn't have a site permission level, it is a hidden group. The permission level shown in parentheses is on item level. If the sharing link is active, the group is assigned to the item. The web part shows information about the item like the name "Document1" and in the tooltip the link type.
  4. **Inactive sharing links:** See picture group 4. If the sharing link is broken or the item is deleted, the group still exists, but it is not assigned to an item. The web part shows just the name of the SharePoint group. This is explained below.
  5. **Limited Access System group** : See picture group 5. The Limited Access permission is assigned to a user automatically by SharePoint when you give permission to the user to access a specific content item. But the user does not have permission to open or edit any other items in the library. You cannot assign this permission level to users or SharePoint groups.

#### Information about Sharing groups 
  {{< figure src="/V1.1.0/images/Special02.png" class="right250" >}}

If you share an item in a SharePoint list, you have 4 options how to share the item:

- Anyone with the link
- People in your Organization with the link
- People with existing access
- Specific people

You can choose if user can read or edit the item.

**Anyone with the link**

This option needs to be enabled in the Admin center. The name of the created group contains "Anonymous", because anyone can access the item, and "View" for the read permission.

  {{< figure src="/V1.1.0/images/Special03.png" class="left600" >}}


**People in your Organization with the link**

The name of the created group contains "Organization", because only people in your organization can access the item, and "Edit" for the edit permission.

  {{< figure src="/V1.1.0/images/Special04.png" class="left600" >}}

**People with existing access**

This option is just to send a link to specified user. No SharePoint group is created.

**Specific people**

With this option, only invited people can access the item. The name of the created group contains "Flexible", because you can change the permissions of this group to edit or read.

  {{< figure src="/V1.1.0/images/Special05.png" class="left600" >}}

{{< rawhtml >}}
</div>
{{</ rawhtml >}}
