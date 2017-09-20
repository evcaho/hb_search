---
layout: page
title: "Search"
category: guide
---

#Honeybadger Search Documentation
Honeybadger's search lets your team powerfully search errors to resolve quickly. You can search errors in one project or across all projects. 

Searches can be done through the search box or keyboard shortcuts when the search box is unselected. Key:value tokens may be combined to refine results, and may also be combined with a full-text query. 

Key:value tokens can appear in the search box in any order. 

##Keyboard shortcuts
Search errors by these keyboard shortcuts outside of the search box: 

| Key      | Response  |
| ------------- |:-------------:| 
| / | Focus search box | 
| A or a | Show resolved And Unresolved Errors| 
| U or u | Show Unresolved Errors|
| R or r | Show Resolved Errors| 
| M or m	| Show Errors Assigned to Me|
| T or t|	Show All Users' Errors|
| J or j | Jump to another project | 
| E or e | Show errors in all environments *| 
**Use first character of environment name to filter by environment.*

##Search box
Enter key:value tokens into the search box to refine results. Multiple tokens may be combined, and may also be combined with an optional full-text query: `john class:UserError -tag:wip -tag:pending component:UsersController action:update`.

Tokens are separated by spaces and are denoted by green highlighting, or yellow highlighting if the query does not match a preset key:value token. 

The default search tokens are `-is:resolved -is:ignored`, which will show all errors that are not resolved or ignored. 
***Add picture***.

###Text search
Search through your errors by **class** or error **message** by going to your project page and typing your search term into the search box. Text queries can also be combined with key:value tokens: 
`john class:UserError -tag:wip -tag:pending component:UsersController action:update`.

***Add picture***.
###Search box keyboard shortcuts
 Key      | Response  |
| ------------- |:-------------:| 
| enter | submits form |
| tab | tabs to next token and selects value inside quotes | 
| shift-tab | reverse-cycles selected token| 
| tab to beginning of line | adds placeholder ("...")| 
| tab out of placeholder | removes placeholder|
| mod backspace | deletes selected token| 
| escape | closes hint| 
| typing | triggers autocomplete |

###Search palette 
Use the search palette to refine your query. Query tokens are separated by spaces and are denoted by green highlighting, or yellow highlighting if the query is not ***Something something something***. 

***add picture of search query with lots of tokens***

###Resolved, ignored, paused
| Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| Resolved | Resolved | `is:resolved`| 
| Not resolved | Unresolved | `-is:resolved` |
| Paused | Paused| `is:paused` |
| Not paused | Unpaused  |`-is:paused` |
| Ignored| Ignored  |`is:ignored` |
| Not ignored | Not ignored  |`-is:ignored` |

Example: 
***Add picture resolved ignored paused***.

Generates errors that are paused, unresolved, and ignored. 

###Assigned to
Errors can be assigned to team members, and results can be refined by assignment.

| Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| Me | Assigned to you | `assignee:"me"`| 
| Nobody | Unassigned | `assignee:"nobody"` |
| Anybody | Assigned to anyone| `assignee:"anybody"` |
| Other | Assigned to one team member |`assignee:""` |

If other, choose a team member from the dropdown list or begin typing.

***Add gif assignee options***.

###Environment
Search errors by your development environment:

| Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| Production | In production | `environment:"production"`| 
| Development| In development | `environment:"development"` |
| Other | In another environment | `environment:"development"` |


If other, choose an environment from the dropdown list or begin typing.

***Add gif environment***.

###Last Occurred
Search errors by their last occurrance. Last Occurred can also be combined with First Seen to create a date range. User's timezone is automatically determined but can be changed manually. 

| Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| Last 24 Hours | From the last 24 hours | `occurred.after:"24 hours ago"`|
| Last 7 Days| From the last 7 days | `occurred.after:"7 days ago"` |
| Since Deploy* | Since last deploy | `occurred.after:"YYYY-MM-DD 19:19 UTC"` |
| Other | Custom date | `occurred.after:"YYYY-MM-DD 0:00 UTC-7"` |

*Since Deploy will not appear if deploy has not occurred.

You can also enter human-friendly dates like `today`, `this week`, or `July 1`, for example: `occurred.after:"this week"`. 

**Add gif last occurred**


###First Seen
Search errors by when they were first seen. First Seen can also be combined with Last Occurred to create a date range. User's timezone is automatically determined but can be changed manually. 

| Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| Last 24 Hours | First seen in the last 24 hours | `created.after:"24 hours ago"`| 
| Last 7 Days| First seen in the last week | `created.after:"7 days ago"` |
| Since Deploy* | First seen since last deploy | `created.after:"YYYY-MM-DD 19:19 UTC"` |
| Other | Custom date | `created.after:"YYYY-MM-DD 0:00 UTC-7"` |
*Since Deploy will not appear if deploy has not occurred.


You can also enter human-friendly dates like `today`, `this week`, or `July 1`, for example: `created.after:"September 12"`.

###Error details
Search error details by class, tag, and message. 

 Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| Class | containing class name | `class:"PermissionDeniedError"`| 
| Tag| containing tag name | `tag:"tag_example"` |
| Message | containing message text | `message:"404"` |

Class, tag, and message can be combined for specific results. For example, the query: `message:"NameError" class:"TextOrganizer" tag:"priority"` searches errors containing "NameError" from the TextOrganizer class with a "priority" tag. 

###Location
Search errors by component, action, URL, and host.  

 Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| Control | in Control | `component:"UsersController"`| 
| Action| in Action | `action:"new"`  |
| URL | in URL | `request.url:"/docs"` |
| Host | in Host | `request.host:"Example"` |

component:"" request.host:"" request.url:"" action:"" 

Locations can be combined for more specific results. For example, `component:"UsersController" action:"new" request.url:"/docs"` searches errors generated from the new action in the UsersController in the /docs.

###Request


##Sorting

##filtering

##batch resolving

