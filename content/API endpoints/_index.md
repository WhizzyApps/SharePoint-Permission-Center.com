---
title: "API endpoints"
date: 2021-03-01T14:39:08-06:00
draft: false
weight: 02
---
Karsten Held, Samuel Gross, 10.02.2021

**Where does the data come from?**

The web part interacts with two APIs: SharePoint REST API and MS Graph API. 

This page explains all endpoints used by the following methods: 

- A) SharePoint API get
- B) SharePoint API post
- C) MS Graph API get

### A) SharePoint API **get** requests

#### Preparing web part

- To get access to the SharePoint API, SPFX needs the object spHttpClient from the web part context.
  - I.e. the get method is accessable like this: `this.context.spHttpClient.get()`
  - The context is accessible in the main *.ts file "PermissionCenterWebPart.ts". 
  - Put the spHttpClient in the web part props: `spHttpClient: this.context.spHttpClient`, see below.
- To get access to the URL of the site, SPFX needs the object pageContext from the web part context.
  - Put the site URL in the web part props: `siteCollectionURL: this.context.pageContext.web.absoluteUrl`, see below.
  
Example in ../src/webparts/PermissionCenter/PermissionCenterWebPart.ts file:
```
export default class PermissionCenterWebPart extends BaseClientSideWebPart<IPermissionCenterWebPartProps> {

  public render(): void {
    const element: React.ReactElement<IPermissionCenterProps> = React.createElement(
      PermissionCenter,
      {
        description: this.properties.description,
        spHttpClient: this.context.spHttpClient,
        siteCollectionURL: this.context.pageContext.web.absoluteUrl
      }
    );
  }
}
```

- The web part props need to be declared in the interface file "IPermissionCenterProps.ts", see below:

Example in IPermissionCenterProps.ts
```
import { SPHttpClient } from '@microsoft/sp-http';

export interface IPermissionCenterProps {
  description: string;
  spHttpClient?: SPHttpClient;
  siteCollectionURL?: string;
}
```
- Then you can access the spHttpClient in the PermissionCenter.tsx file within the web part props: `this.props.spHttpClient`, see below:

#### Example for API calls

Example function for Typescript-React in PermissionCenter.tsx file:

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

Call _spApiGet(url) from another function with the parameter "url":

The site URL is accessible in the web part props: `this.props.siteCollectionURL`

```
public async componentDidMount() {
  const url = this.props.siteCollectionURL + "/_api/web/currentuser/isSiteAdmin";
  const response = await this._spApiGet(url);
  console.log(response);
}
```

#### Endpoints

All endpoints (URLs) use the site URL

- [SITE_URL] = ```https://[YOUR_TENANT].sharepoint.com/sites/[YOUR_SITE]```
- Example: ```https://myTenant.sharepoint.com/sites/mySite```
- For root site: ```https://myTenant.sharepoint.com```

Get current user permissions

- `[SITE_URL]/_api/web/currentuser/isSiteAdmin`
- `[SITE_URL]/_api/web/effectiveBasePermissions`

Get default site groups

- `[SITE_URL]/_api/web/AssociatedOwnerGroup`
- `[SITE_URL]/_api/web/AssociatedMemberGroup`
- `[SITE_URL]/_api/web/AssociatedVisitorGroup`

Get all site groups

- `[SITE_URL]/_api/web/sitegroups`

Get members with access given directly

- `[SITE_URL]/_api/web/RoleAssignments?$expand=Member,RoleDefinitionBindings`

Get site admins

- `[SITE_URL]/_api/web/siteusers?$filter=IsSiteAdmin%20eq%20true`

Get group permissions

- `[SITE_URL]/_api/Web/RoleAssignments/GetByPrincipalId([GROUP_ID])/RoleDefinitionBindings`
- [GROUP_ID] = id of SharePoint group in API
- `[SITE_URL]/_api/Web/RoleAssignments/GetByPrincipalId(3)/RoleDefinitionBindings`

Get group members

- `[SITE_URL]/_api/web/SiteGroups/GetById([GROUP_ID])/users`
- [GROUP_ID] = id of SharePoint group in API
- Example: ```[SITE_URL]/_api/web/SiteGroups/GetById(3)/users```

Get all site permission levels

- `[SITE_URL]/_api/web/roleDefinitions`

Get properties of sharing groups

- `[SITE_URL]/_api/search/query?querytext='[GUID]'`
- [GUID] = Globally Unique Identifier of sharing group in API
- Example: `[SITE_URL]/_api/search/query?querytext='6B29FC40-CA47-1067-B31D-00DD010662DA'`


Get all groups, that have permission levels

- `[SITE_URL]/_api/Web/RoleAssignments`

Get id of shared item to open permissions page of shared item

- `[SITE_URL]/_api/web/Lists('[LIST_ID]')/GetItemByUniqueId('[GUID]')`
- Example: `[SITE_URL]/_api/web/Lists('804fdfed-3b60-4f61-90b2-0a8f82b44395')/GetItemByUniqueId('00761165-1514-4A40-A4B9-32A0A9709069')`
- link to open the permissions page of a shared item:
- `[SITE_URL]/_layouts/15/user.aspx?obj=%7B[LIST_ID]%7D,[SharePoint_ID],LISTITEM`
- Example: `[SITE_URL]/_layouts/15/user.aspx?obj=%7B804fdfed-3b60-4f61-90b2-0a8f82b44395%7D,17,LISTITEM`

Get user by loginName

- `[SITE_URL]/_api/web/siteusers(@v)?@v='${encodeURIComponent([USER_LOGINNAME])}'`
- Example: `[SITE_URL]/_api/web/siteusers(@v)?@v='${encodeURIComponent('i:0#.f|membership|donald.duck@myTenant.com')}'`

### B) SharePoint API **post** requests

#### Properties of sharing groups

- Get properties of sharing groups via post
- `[SITE_URL]/_api/web/Lists('[LIST_ID]')/GetItemByUniqueId('[GUID]')/GetSharingInformation?$Expand=permissionsInformation`
- Example: ```[SITE_URL]/_api/web/Lists('804fdfed-3b60-4f61-90b2-0a8f82b44395')/GetItemByUniqueId('F5B3CBF9-055A-41EC-9245-5F13D572BFC8')/GetSharingInformation?$Expand=permissionsInformation```

Example function for Typescript-React in PermissionCenter.tsx file:

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

Call _spApiGet(url) from another function with the parameter "url".

```
public async componentDidMount() {
  const url = this.props.siteCollectionURL + "/_api/web/Lists('[LIST_ID]')/GetItemByUniqueId('[GUID]')/GetSharingInformation?$Expand=permissionsInformation"
  const response = await this._spApiPost(url);
  console.log(response);
}
```

#### Delete group

- `[SITE_URL]/_api/web/sitegroups/removebyid([GROUP_ID])`
- [GROUP_ID] = id of SharePoint group in API
- Example: `[SITE_URL]/_api/web/sitegroups/removebyid(14)`

Example function for Typescript-React in PermissionCenter.tsx file:

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
    return response;
  }
}
```
Call _spApiGet(url) i.e. from another function with the parameter "url".
```
public async componentDidMount() {
  const url = this.props.siteCollectionURL + "/_api/web/sitegroups/removebyid(14)";
  const response = await this._spApiPost(url);
  console.log(response);
}
```

#### Delete sharing group

- `[SITE_URL]/_api/web/Lists('[LIST_ID]')/GetItemByUniqueId('[ITEM_ID]')/UnshareLink`
  - [ITEM_ID] = GUID of item. Example: `00761165-1514-4A40-A4B9-32A0A9709069`
  - [LIST_ID] = ID of list (folder) the item is in. Example: `804fdfed-3b60-4f61-90b2-0a8f82b44395`
- `body = { shareId: [SHARE_ID] }`
  - [SHARE_ID] = last GUID of loginName of SharePoint group 
  - Example loginName: `SharingLinks.00761165-1514-4a40-a4b9-32a0a9709069.OrganizationEdit.dcdfc2bc-fb41-4f93-9770-61a49c560c59`
  - Example [SHARE_ID]: `dcdfc2bc-fb41-4f93-9770-61a49c560c59`

Example function for Typescript-React in PermissionCenter.tsx file:

``` 
import { SPHttpClient, ISPHttpClientOptions} from '@microsoft/sp-http';

// main class in PermissionCenter.tsx file
export default class PermissionCenter extends React.Component<IPermissionCenterProps, {}> {

  // function for API call
  private async _deleteSharingGroup (): Promise<object> {

    const listId = '804fdfed-3b60-4f61-90b2-0a8f82b44395';
    const itemId = '00761165-1514-4A40-A4B9-32A0A9709069';
    const shareId = 'dcdfc2bc-fb41-4f93-9770-61a49c560c59';
    const url = this.props.siteCollectionURL + `/_api/web/Lists('${listId}')/GetItemByUniqueId('${itemId}')/UnshareLink`;

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
    return response;
  }
}
```

Call _deleteSharingGroup() i.e. from another function.
```
  public async componentDidMount() {
    const response = await this._deleteSharingGroup();
    console.log(response);
  }
```

#### Ensure user

- To ensure that user has a profile in SharePoint. If not, a profile will be created
  - `[SITE_URL]/_api/web/ensureuser`
  - `body: {'logonName': userLoginName}`
  - Example: `body: {'logonName': 'i:0#.f|membership|dagobert.duck@myTenant.com'}`

Example function for Typescript-React in PermissionCenter.tsx file:

``` 
import { SPHttpClient, ISPHttpClientOptions} from '@microsoft/sp-http';

// main class in PermissionCenter.tsx file
export default class PermissionCenter extends React.Component<IPermissionCenterProps, {}> {
  
  private async _ensureUser (userLoginName) {
    
    // parameter
    let ensureAdminUrl = this.props.siteCollectionURL + `/_api/web/ensureuser`;
    const ensureAdminOpts: ISPHttpClientOptions = {
      headers: {
        'Accept': 'application/json;odata=nometadata',
        'Content-type': 'application/json;odata=verbose',
        'odata-version': '',
      },
      body: JSON.stringify({
        'logonName': userLoginName
      }),
      mode: 'cors'
    };

    // http request
    return await this.props.spHttpClient.post(ensureAdminUrl, SPHttpClient.configurations.v1, ensureAdminOpts);
  }
}
```

Call _ensureUser(userLoginName) i.e. from another function.
```
  public async componentDidMount() {
    const userLoginName = 'i:0#.f|membership|donald.duck@myTenant.com';
    const response = await this._ensureUser(userLoginName);
    console.log(response);
  }
```

#### Add/ remove admin

- To Add/ remove user to/from admins, post user by setting attribute "isSiteAdmin" = true/false
- `[SITE_URL]/_api/web/GetUserById([USER_ID])`
- Example: `[SITE_URL]/_api/web/GetUserById(22)`

Example function for Typescript-React in PermissionCenter.tsx file:

``` 
import { SPHttpClient, ISPHttpClientOptions} from '@microsoft/sp-http';

// main class in PermissionCenter.tsx file
export default class PermissionCenter extends React.Component<IPermissionCenterProps, {}> {

  /* 
    function for API call with parameters 
    userId: SharePoint ID of user
    isRemove: if remove user from admins isRemove=true, if add isRemove=false
  */
  private async _addOrRemoveAdmin (userId, isRemove) {
    
    // parameter
    let requestUrl = this.props.siteCollectionURL + `/_api/web/GetUserById(${userId})`;
    let dataToPost = JSON.stringify({
      '__metadata': { 'type': 'SP.User' },
      'IsSiteAdmin': isRemove ? 'false' : 'true',
    });
    const spOpts: ISPHttpClientOptions = {
      headers: {
        'Accept': 'application/json;odata=nometadata',
        'Content-type': 'application/json;odata=verbose',
        'odata-version': '',
        "X-HTTP-Method": "MERGE"
      },
      body: dataToPost,
      mode: 'cors'
    };

    // http request
    const response = await this.props.spHttpClient.post(requestUrl, SPHttpClient.configurations.v1, spOpts);
    return response;
  }
}
```

Call _addOrRemoveAdmin(userId, isRemove) i.e. from another function.
```
  public async componentDidMount() {
    const userId = 22;
    const isRemove = false;
    const response = await this._addOrRemoveAdmin(userId, isRemove);
    console.log(response);
  }
```

#### Add /remove user

Add /remove user to/from SharePoint group:

- Add: `[SITE_URL]/_api/web/sitegroups/getbyid([GROUP_ID])/users`
  - Example: `[SITE_URL]/_api/web/sitegroups/getbyid(4)/users`
  - `body: {'loginName': userLoginName}`
  - Example: `body: {'loginName': 'i:0#.f|membership|dagobert.duck@myTenant.com'}`
- Remove: `[SITE_URL]/removeByLoginName`
  - `body: {'loginName': userLoginName}`

Example function for Typescript-React in PermissionCenter.tsx file:

``` 
import { SPHttpClient, ISPHttpClientOptions} from '@microsoft/sp-http';

// main class in PermissionCenter.tsx file
export default class PermissionCenter extends React.Component<IPermissionCenterProps, {}> {
  /* 
  function for API call with parameters 
  userLoginName: loginName of user
  groupId: SharePoint ID of group
  isRemove: if remove user from admins isRemove=true, if add isRemove=false
  */
  private async _addOrRemoveUserFromSpGroup (userLoginName, groupId, isRemove) {
    // parameter
    // for add user
    let requestUrl = this.props.siteCollectionURL + `/_api/web/sitegroups/getbyid(${groupId})/users`;
    let dataToPost = JSON.stringify({
      '__metadata': { 'type': 'SP.User' },
      'LoginName': userLoginName
    });
    // for remove user
    if (isRemove) {requestUrl += "/removeByLoginName";}
    if (isRemove) {
      dataToPost = JSON.stringify({
        'loginName': userLoginName
      });
    }
    // general
    const spOpts: ISPHttpClientOptions = {
      headers: {
        'Accept': 'application/json;odata=nometadata',
        'Content-type': 'application/json;odata=verbose',
        'odata-version': ''
      },
      body: dataToPost,
      mode: 'cors'
    };
  
    // http request
    const response = await this.props.spHttpClient.post(requestUrl, SPHttpClient.configurations.v1, spOpts);
    return response;
  }
}
```

Call _addOrRemoveUserFromSpGroup(userLoginName, groupId, isRemove) i.e. from another function.
```
  public async componentDidMount() {
    const userLoginName = 'i:0#.f|membership|donald.duck@myTenant.com';
    const groupId = 22;
    const isRemove = false;
    const response = await this._addOrRemoveUserFromSpGroup(userLoginName, groupId, isRemove);
    console.log(response);
  }
```

#### Delete user from site

- `[SITE_URL]/_api/web/GetUserById([USER_SP_ID])`
- Example: `[SITE_URL]/_api/web/GetUserById(15)`
- header: `'X-HTTP-Method': 'DELETE'`

Example function for Typescript-React in PermissionCenter.tsx file:

``` 
import { SPHttpClient, ISPHttpClientOptions} from '@microsoft/sp-http';

// main class in PermissionCenter.tsx file
export default class PermissionCenter extends React.Component<IPermissionCenterProps, {}> {

  // function for API call with parameters 
  private async _deleteUserFromSite (userId) {

    // parameter
    const spOpts: ISPHttpClientOptions = {
      headers: {
        'Accept': 'application/json;odata=nometadata',
        'Content-type': 'application/json;odata=verbose',
        'odata-version': '',
        'X-HTTP-Method': 'DELETE'
      },
      mode: 'cors'
    };
    const requestUrl = this.props.siteCollectionURL + `/_api/web/GetUserById(${userId})`;
    // http request
    const response = await this.props.spHttpClient.post(requestUrl, SPHttpClient.configurations.v1, spOpts);
    return response;
  }
}
```

Call _deleteUserFromSite (userId) i.e. from another function.
```
  public async componentDidMount() {
    const userId = 114;
    const response = await this._deleteUserFromSite (userId);
    console.log(response);
  }
```

### C) Graph API get requests

#### Preparing web part

- To get access to the Graph API, SPFX needs the object msGraphClientFactory from the web part context.
- I.e. the getClient method is accessable like this: `this.props.context.msGraphClientFactory.getClient()`
- The context is accessible in the main *.ts file "PermissionCenterWebPart.ts". 
- Put the context in the web part props: `context: this.context`, see below.
  
Example in src/webparts/PermissionCenter/PermissionCenterWebPart.ts file:
```
export default class PermissionCenterWebPart extends BaseClientSideWebPart<IPermissionCenterWebPartProps> {

  public render(): void {
    const element: React.ReactElement<IPermissionCenterProps> = React.createElement(
      PermissionCenter,
      {
        description: this.properties.description,
        context: this.context,
      }
    );
  }
}
```

- The web part props need to be declared in the interface file "IPermissionCenterProps.ts", see below:

Example in IPermissionCenterProps.ts
```
import { WebPartContext } from '@microsoft/sp-webpart-base';

export interface IPermissionCenterProps {
  description: string;
  context?: WebPartContext;
}
```
- Then you can access the context in the PermissionCenter.tsx file within the web part props: `this.props.context`, see below:

#### Example for API calls

Example function for Typescript-React in PermissionCenter.tsx file:

``` 
import { MSGraphClient } from '@microsoft/sp-http';

// main class in PermissionCenter.tsx file
export default class PermissionCenter extends React.Component<IPermissionCenterProps, {}> {

  // get data from Microsoft Graph API
  private _graphApiGet (url: string): Promise<any> {

    return new Promise<any> (
      (resolve, reject) => {
        this.props.context.msGraphClientFactory.getClient()
        .then(
          (client: MSGraphClient): any => {
            client.api(url).get(
              async (error, response: any) => {
                if (response) {
                  resolve(response);
                } 
                else if (error) {
                  reject(error);
                }
              }
            );
          }
        )
      }
    )
  }
}
```

Call _graphApiGet(url) from another function with the parameter "url":

```
public async componentDidMount() {
  const url = "/organization";
  const response = await this._graphApiGet(url);
  console.log(response);
}
```

#### Endpoints

Get name of organization of tenant

- `/organization`

Get properties of Azure groups

- `/groups/[AZURE_GROUP_ID]`
- Example: `/groups/d2d7dbb8-3e81-4783-b863-0706748b93c4`

Get members of Azure groups

- `/groups/[AZURE_GROUP_ID]/members`
- Example: `/groups/d2d7dbb8-3e81-4783-b863-0706748b93c4/members`

Get owners of Azure groups

- `/groups/[AZURE_GROUP_ID]/owners`
- Example: `/groups/d2d7dbb8-3e81-4783-b863-0706748b93c4/owners`

Get Azure properties for user

- `/users/[USER_PRINZIPAL_NAME]`
- Example: `/users/donald.duck@myTenant.com`

