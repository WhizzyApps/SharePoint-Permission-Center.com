---
title: "Version 1.0.1.0"
date: 2021-03-01T14:39:08-06:00
draft: false
---
Samuel Gross, 04.03.2021

## Release notes

- All SharePoint system groups are now shown in the web part. For example: SharePoint Administrator&quot;, SharePoint Service Administrator&quot;, Company Administrator&quot;, &quot;Everyone Except external users&quot;. They are listed as a user and can be managed via user card: &quot;change membership&quot; and &quot;delete user from site&quot;.
- Usernames are sorted not just as a string:
  - mutated vowel: oe is treated as o, etc.
  - numbers as numbers: 2 before 10
- SharePoint Api call to get members of azure groups: get 500 users per request, instead of 1000.
- User card expands without animation by default. Switch it on in debug mode.

## Web part description

### Configuration page 1/2
<img src="/images/15 Configuration 1 v1.0.1.0.png" style="width:250px;"/>

### Configuration page 2/2
<img src="/images/16.1 Configuration 3 v1.0.1.0.png" style="width:250px; float:right"/>


The debug page is for developers to log the following to the developer console in case of bugs. By default it is switched off.

- Log state: react has a variable called &quot;state&quot;. When the web part has finished loading, the last state will be logged.
- Throw errors: by default all errors are catched. Enabled it to rethrow them.
- Log errors. By default all errors are catched and not logged. Enable it to log them to the console.
- Log variables of PermissionCenter.tsx: This is the main react component in the source code. If enabled, the most important variables of most functions are logged.
- Log variables of other components: Enable to log most important variables of most functions of all other react components.
- Use animate height for user card: Sometimes the user card doesn&#39;t expand. Disable it to try to expand it without animation.
