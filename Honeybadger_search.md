---
layout: page
title: "Search"
category: guide
---

# Honeybadger Search Documentation
Honeybadger lets you search errors in one project or across all projects using the search builder. `key:value` tokens may be combined to refine results, and may also be combined with a free-form text query. 

`key:value` tokens can appear in the search box in any order. 

## How combined tokens filter results
Positive tokens use AND to match results unless the same field is used multiple times. For example, a search for `class:"Foo" class:"Bar" ` will include errors with class `Foo` OR `Bar`.

Searches can be negated by prepending "-" to any field name. Negative tokens (which begin with a minus sign: `-`) **always** use AND, so that `"-class:Foo -class:Bar"` will return results which are not class `Foo` AND not class `Bar`.

Example query     | Searches  |
| ------------- |:-------------:| 
|  `class:"Foo" is:resolved` | Resolved errors with class `Foo`| 
| `-class:"Foo" is:resolved` | Resolved errors without class `Foo` | 
| `-class:"Foo" -is:resolved` | Unresolved errors with class `Foo`| 
| `class:"Foo" class:"Bar" is:resolved` | Resolved errors with class `Foo` OR class `Bar`| 
| `-class:"Foo" -class:"Bar" is:resolved` | Resolved errors without class `Foo` AND class `Bar` |

## Ways to search

Use the search builder to create a query. A query can include many `key:value` tokens for refined results or none. Query tokens are separated by spaces and are denoted by green highlighting, or yellow highlighting if the query is not a `key:value` token. 

![Image of search box and search palette](images/search_palette.png)

## Search builder

Enter `key:value` tokens into the search box to refine results. Multiple tokens may be combined, and may also be combined with a free form text query. 

Example query:
`john class:UserError -tag:wip -tag:pending component:UsersController action:update`.

Tokens are separated by spaces and are denoted by green highlighting. Highlighting will be yellow if the query doesn't match `key:value` token format, like [free-form text](## Free-form text search).  

The search box is populated by default with `-is:resolved -is:ignored`, which will show all errors that are not resolved or ignored. 

![Image of default search box values](images/isresolved_isnotignored.png)

## Search by keyboard shortcuts 

Use the following keyboard shortcuts in the search box to write or refine your query. 

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


## Search by resolved, ignored, or paused

Search errors that are resolved, ignored, paused, or unresolved, not ignored, or unpaused. 

| Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| resolved | Resolved | `is:resolved`| 
| -resolved | Unresolved | `-is:resolved` |
| paused | Paused| `is:paused` |
| -paused | Unpaused  |`-is:paused` |
| ignored| Ignored  |`is:ignored` |
| -ignored | Not ignored  |`-is:ignored` |

Example: 
![Image of resolved, ignored, and paused requests](images/resolved_ignored_paused.png).

Generates errors that are paused, unresolved, and ignored. 

## Search by assignee

Errors can be assigned to team members, and results can be refined by assignment. Tokens can be combined to search errors assigned to multiple team members. 

| Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| me | Assigned to me | `assignee:"me"`| 
| -me| Not assigned to me| `-assignee:"me"`|
| nobody | Unassigned | `assignee:"nobody"` |
| anybody | Assigned to anyone| `assignee:"anybody"` |
| other | Assigned to one team member |`assignee:""` |
| -other| Not assigned to one team member| `-assignee:""`|

If other, choose a team member from the dropdown list or begin typing to trigger autocomplete.

![Animation of assigned to menu](images/assigned_to.gif).

## Search by environment

Search errors by your environment:

| Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| production | In production | `environment:"production"`| 
| not production | Not in production | `-environment:"production"`|
| development| In development | `environment:"development"` |
| except development| Not in development | `-environment:"development"` |
| other | In another environment | `environment:"test"` |

If other, choose an environment from the dropdown list or begin typing to trigger autocomplete.

![Animation of assigned to menu](images/environment.gif).

## Search by last occurred

Search errors by their last occurrance. A last occured query and a negative (-) last occurred token can be combined to create a date range. Your timezone is automatically determined but can be changed manually.  

| Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| last 24 hours | From the last 24 hours | `occurred.after:"24 hours ago"`|
| -last 24 hours | Before the last 24 hours | `occurred.before:"24 hours ago"`|
| last 7 days| From the last 7 days | `occurred.after:"7 days ago"` |
| -last 7 days| Before the last 7 days | `occurred.before:"7 days ago"` |
| since deploy* | Since last deploy | `occurred.after:"YYYY-MM-DD 19:19 UTC"` |
| -since deploy | Before last deploy | `occurred.after:"YYYY-MM-DD 19:19 UTC"` |
| other | Custom date | `occurred.after:"YYYY-MM-DD 0:00 UTC-7"` |

*If deploy hasn't happened, Since Deploy won't autopopulate with a date.

You can also enter human-friendly dates like `today`, `this week`, or `July 1`, for example: `occurred.after:"this week"`. 

![Animation of last occurred query](images/last_occurred.gif)


## Search by first seen

Search errors by when they were first seen. A first seen query and a negative (-) first seen query can be combined to create a date range. Your timezone is automatically determined but can be changed manually.  

| Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| last 24 Hours | First seen in the last 24 hours | `created.after:"24 hours ago"`| 
| -last 24 hours | First seen before 24 hours ago | `created.before:"24 hours ago"`|
| last 7 days| First seen in the last week | `created.after:"7 days ago"` |
| last 7 days| First seen in the last week | `created.before:"7 days ago"` |
| since deploy* | First seen since last deploy | `created.after:"YYYY-MM-DD 19:19 UTC"` |
| other | Custom date | `created.after:"YYYY-MM-DD 0:00 UTC-7"` |

*Since Deploy will not appear if deploy has not occurred.

You can also enter human-friendly dates like `today`, `this week`, or `July 1`, for example: `created.after:"September 12"`.

## Search by error details
Search error by class, tag, and message. 

 Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| class | With a certain class | `class:"PermissionDeniedError"`| 
| -class| Without a certain class | `-:"PermissionDeniedError"`|
| tag| With a certain tag name | `tag:"tag_example"` |
| -tag| Without a certain tag name | `-tag:"tag_example"` |
| message | With a message | `message:"404"` |
| -message | Without message text | `-message:"404"` |

Class, tag, and message can be combined for specific results. For example, the query: `message:"NameError" class:"TextOrganizer" tag:"priority"` searches errors containing "NameError" from the TextOrganizer class with a "priority" tag. 

## Search by location
Search errors by component, action, URL, and host.  

 Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| control | With a controller/component | `component:"UsersController"`| 
| -control | Without a controller/component | `-component:"UsersController"`| 
| action| With an action | `action:"update"`  |
| -action| Without an action | `-action:"update"`  |
| url | That happened at the specified URL| `request.url:"camera"` |
| -url | That happened without specified URL| `-request.url:"camera"` |
| host | On a server with this name | `request.host:"Example"` |
| -host | Not on a server with this name | `request.host:"Example"` |

Locations can be combined for more specific results. For example, the query: `component:"UsersController" action:"update" request.url:"/docs"` searches errors generated from the update action in the UsersController in the URL `camera`.

## Search by request
Search errors by context, params, user agent, or session hashes. 

 Name       | Matches errors   | Example  |
| ------------- |:-------------:| -----:|
| context | Within a context  | `context.user.email:"bob@example.io"`| 
| -context| Without a context | `-context.user.name:"Bob"`|
| params | Within a parameter | `params.user.first_name:"Bob"`|
|-params | Without a parameter | `params.old:"useless"`|
|user agent | triggered by a user agent | `request.user_agent:"Googlebot`|
|-user agent | not triggered by a user agent | `-request.user_agent:"Googlebot`|

Requests can be combined or nested for more specific results.  For example, searching for context.user.email:bob@example.com would match the following hash that was sent in the context with an error:

`{ user: { email: "bob@example.com" } } `

When searching these hashes, separate the nested levels of the hash with a period. For example `params.user.first_name:bob`.

Searches against context, param, user agent, or session hashes use * as a wildcard, so a search for `context.user.email:*@example.com` would match any email address at example.com.

## Sorting results
Error results  can be sorted by date or error count.

### Sort by date
Sorting by "Last seen" lets you quickly jump to the newest or oldest exceptions that match your search result.

1. Go to your project's error list page
2. Click on the table header labeled "last seen"
3. Click on it again to reverse the sort order 

![Image of sort by date button](images/toggle_sort_order.png) 

### Sort by count
Sorting by "Times" lets you see which errors have happened the most or the fewest times.

1. Go to your project's error index
2. Click on the table header labeled "times"
3. Click on it again to reverse the sort order

![Image of sort by count button](images/toggle_count_order.png)


## Update all
Errors can be grouped and batch resolved or unresolved. 

1. Use the search to select which errors you'd like to bulk resolve.
2. Click on "Update All" and choose an option from the dropdown.

![Image of update all dropdown](images/Update_all.png)

## Free-form text search

Search through your errors by **class** or error **message** by typing your search term into the search box. Free-form text queries can also be combined with `key:value` tokens, for example: 
`john class:UserError component:UsersController action:update`.

## Keyboard shortcuts

Quickly search errors using these keyboard shortcuts: 

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
