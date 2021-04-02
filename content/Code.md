
### Where does the data come from?

#### SharePoint API **get** request:

Example function for Typescript-React in *.tsx file:

``` 
import { SPHttpClient, ISPHttpClientOptions} from '@microsoft/sp-http';

// main class in PermissionCenter.tsx file
export default class PermissionCenter extends React.Component<IPermissionCenterProps, {}> {

  // function for API call
  private async _spApiGet (url: string): Promise<object> {
    const clientOptions: ISPHttpClientOptions = {
      headers: new Headers(),
      method: 'GET',
      mode: 'cors'
    };
    const response = await this.props.spHttpClient.get(url, SPHttpClient.configurations.v1, clientOptions);
    const responseJson = await response.json();
    return responseJson;
  }
}
```

Call _spApiGet(url) from another funcion with the parameter "url":


```
public async componentDidMount() {
  const url = https://[YOUR_TENANT].sharepoint.com/sites/[YOUR_SITE]/_api/web/currentuser/isSiteAdmin
  const response = await _spApiGet(url);
  console.log(response);
}
```
**Endpoints (urls) used in web part**
with
- [SITE_URL] = ```https://[YOUR_TENANT].sharepoint.com/sites/[YOUR_SITE]```
- Example: ```https://myTenant.sharepoint.com/sites/mySite```

Get current user permissions

- `[SITE_URL]/_api/web/currentuser/isSiteAdmin`
- `[SITE_URL]/_api/web/effectiveBasePermissions`

Get default site groups:

- `[SITE_URL]/_api/web/AssociatedOwnerGroup`
- `[SITE_URL]/_api/web/AssociatedMemberGroup`
- `[SITE_URL]/_api/web/AssociatedVisitorGroup`

Get all site groups:

- `[SITE_URL]/_api/web/sitegroups`

Get members with access given directly:

- `[SITE_URL]/_api/web/RoleAssignments?$expand=Member,RoleDefinitionBindings&amp;$filter=Member/PrincipalType%20ne%208`

Get site admins:

- `[SITE_URL]/_api/web/siteusers?$filter=IsSiteAdmin%20eq%20true`

Get group permissions:

- `[SITE_URL]/_api/Web/RoleAssignments/GetByPrincipalId([GROUP_ID])/RoleDefinitionBindings`
- [GROUP_ID] = id of SharePoint group in API
- `[SITE_URL]/_api/Web/RoleAssignments/GetByPrincipalId(3)/RoleDefinitionBindings`

Get group members:

- `[SITE_URL]/_api/web/SiteGroups/GetById([GROUP_ID])/users`
- [GROUP_ID] = id of SharePoint group in API
- Example: ```[SITE_URL]/_api/web/SiteGroups/GetById(3)/users```

Get all site permission levels:

- `[SITE_URL]/_api/web/roleDefinitions`

Get properties of sharing groups:

- `[SITE_URL]/_api/search/query?querytext='[GUID]'`
- [GUID] = Globally Unique Identifier of sharing group in API
- Example: `[SITE_URL]/_api/search/query?querytext='6B29FC40-CA47-1067-B31D-00DD010662DA'`


Get all groups, that have permission levels:

- `[SITE_URL]/_api/Web/RoleAssignments`

#### SharePoint API **post** request:

**Get properties of sharing groups in case of link type "specific people"**

- `[SITE_URL]/_api/web/Lists('[LIST_ID]')/GetItemByUniqueId('[GUID]')/GetSharingInformation?$Expand=permissionsInformation`
- Example: ```https://[YOUR_TENANT].sharepoint.com/sites/[YOUR_SITE]/_api/web/Lists('804fdfed-3b60-4f61-90b2-0a8f82b44395')/GetItemByUniqueId('[F5B3CBF9-055A-41EC-9245-5F13D572BFC8]')/GetSharingInformation?$Expand=permissionsInformation```
- Example function for Typescript-React in *.tsx file:

``` 
import { SPHttpClient, ISPHttpClientOptions} from '@microsoft/sp-http';

// main class in PermissionCenter.tsx file
export default class PermissionCenter extends React.Component<IPermissionCenterProps, {}> {

  // function for API call
  private async _spApiPost (url: string): Promise<object> {
    const requestHeaders: Headers = new Headers();  
    requestHeaders.append('Content-type', 'application/json'); 
    requestHeaders.append('Accept', 'application/json'); 
    requestHeaders.append('Authorization', 'Bearer'); 
    
    const clientOptions: ISPHttpClientOptions = {
      headers: requestHeaders,
      method: 'POST',
      mode: 'cors',
    };
    const response = await this.props.spHttpClient.post(url, SPHttpClient.configurations.v1, clientOptions);
    const responseJson = await response.json();
    return responseJson;
  }
}
```
- Call _spApiGet(url) from another funcion with the parameter "url".
```
public async componentDidMount() {
  const url = https://[YOUR_TENANT].sharepoint.com/sites/[YOUR_SITE]/_api/web/Lists('804fdfed-3b60-4f61-90b2-0a8f82b44395')/GetItemByUniqueId('[F5B3CBF9-055A-41EC-9245-5F13D572BFC8]')/GetSharingInformation?$Expand=permissionsInformation
  const response = await _spApiPost(url);
  console.log(response);
}
```

**Delete group**

- ```[SITE_URL]/_api/web/sitegroups/removebyid([GROUP_ID])```
- [GROUP_ID] = id of SharePoint group in API
- Example: ```[SITE_URL]/_api/web/sitegroups/removebyid([3])```
- Example function for Typescript-React in *.tsx file:

``` 
import { SPHttpClient, ISPHttpClientOptions} from '@microsoft/sp-http';

// main class in PermissionCenter.tsx file
export default class PermissionCenter extends React.Component<IPermissionCenterProps, {}> {

  // function for API call
  private async _spApiPost (url: string): Promise<object> {
    const clientOptions: ISPHttpClientOptions = {
        headers: new Headers(),
        method: 'post',
        mode: 'cors'
      };
    const response = await this.props.spHttpClient.post(url, SPHttpClient.configurations.v1, clientOptions);
    const responseJson = await response.json();
    return responseJson;
  }
}
```
- Call _spApiGet(url) from another funcion with the parameter "url".
```
public async componentDidMount() {
  const url = https://[YOUR_TENANT].sharepoint.com/sites/[YOUR_SITE]/_api/web/sitegroups/removebyid(3)
  const response = await _spApiPost(url);
  console.log(response);
}
```

**Delete sharing group**

- `[SITE_URL]/_api/web/Lists('[LIST_ID]')/GetItemByUniqueId('[ITEM_ID]')/UnshareLink`



- Example function for Typescript-React in *.tsx file:

``` 
import { SPHttpClient, ISPHttpClientOptions} from '@microsoft/sp-http';

// main class in PermissionCenter.tsx file
export default class PermissionCenter extends React.Component<IPermissionCenterProps, {}> {

  // function for API call
  private async _spApiPost (url: string): Promise<object> {
    const listId = 
    const itemId = 
    const shareId = 
    const url = `${props.siteCollectionURL}/_api/web/Lists('${listId}')/GetItemByUniqueId('${itemId}')/UnshareLink`;

    const requestHeaders: Headers = new Headers();  
    requestHeaders.append('Content-type', 'application/json'); 
    requestHeaders.append('Accept', 'application/json'); 
    requestHeaders.append('Authorization', 'Bearer'); 

    const body: string = JSON.stringify({
      shareId: shareId
    });
    
    const clientOptions: ISPHttpClientOptions = {
      headers: requestHeaders,
      method: 'POST',
      mode: 'cors',
      body: body
    };
    const response = await this.props.spHttpClient.post(url, SPHttpClient.configurations.v1, clientOptions);
    const responseJson = await response.json();
    return responseJson;
  }
}
```
- Call _spApiGet(url) from another funcion with the parameter "url".
```
public async componentDidMount() {
  const url = https://[YOUR_TENANT].sharepoint.com/sites/[YOUR_SITE]/_api/web/sitegroups/removebyid(3)
  const response = await _spApiPost(url);
  console.log(response);
}
```

**Get id of shared item to open permissions page of item**

- `[SITE_URL]/_api/web/Lists('[LIST_ID]')/GetItemByUniqueId('[GUID]')`

**Add/ remove user to/from admins: post user with attribute "isSiteAdmin" = true/false**

- `[SITE_URL]/_api/web/GetUserById([USER_ID])`
- In case SharePoint id not available: Get SharePoint id of user
  - `[SITE_URL]/_api/web/siteusers(@v)?@v='[USER_LOGIN_NAME]'`
- To add: in case user has no profile in SharePoint: create profile via post
  - `[SITE_URL]/_api/web/ensureuser`

**Add user to group: post with body 'loginName': userLoginName**

- `[SITE_URL]/_api/web/sitegroups/getbyid([GROUP_ID])/users`

**Remove user from group: post with body 'loginName': userLoginName**

- `[SITE_URL]/removeByLoginName`

**Delete user from site: post with header: 'X-HTTP-Method': 'DELETE'**

- `[SITE_URL]/_api/web/GetUserById([USER_SP_ID])`

#### Graph API endpoints:

Get members of Azure groups:

- `/groups/[AZURE_GROUP_ID]/members`

Get owners of Azure groups:

- `/groups/[AZURE_GROUP_ID]/owners`

Get properties of Azure groups:

- `/groups/[AZURE_GROUP_ID]`

Get name of organization of tenant to display it in tooltip for sharing groups

- `/organization`

Get azure properties for user

- `/users/[USER_PRINZIPAL_NAME]`
