#### v1

##### Parameters
id (required, 24 char hex) ... the mobile flow's unique identifier. Required in GET, PUT & DELETE requests.

##### get mobileflow
```
GET /v1/mobileflow/{id}
```
##### Response
```
Status: 200
[MobileFlow][]
```
##### Response
```
Status: 400
```
##### Response
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### delete mobileflow
```
DELETE /v1/mobileflow/{id}
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### update mobileflow
```
PUT /v1/mobileflow/{id}
```
##### Request
```
[MobileFlow][]
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### create mobileflow
```
POST /v1/mobileflow/{id}
```
##### Request
```
[MobileFlow][]
```
##### Response 
```
Status: 200
[MobileFlow][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

#### v2

##### Parameters
id (optional, 24 char hex) ... the mobile flow's unique identifier. Required in GET, PUT & DELETE requests.

##### get mobileflow
```
GET /v2/mobileflow/{id}
```
##### Response 
```
Status: 200
[MobileFlow][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * * 
##### delete mobileflow 
```
DELETE /v2/mobileflow/{id}
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### update mobileflow
```
PUT /v2/mobileflow/{id}
```
##### Request
```
[MobileFlow][]
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### create mobileflow
```
POST /v2/mobileflow/{id}
```
##### Request
```
[MobileFlow][]
```
##### Response 
```
Status: 200
[MobileFlow][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

### MO Routing

#### `moroute` model

| property  | type  | required      | description   |
|-----      |-----  |-----          |-----|
| id        | 24 char hex   | true          | the MO route's ID |
| keyword   | 24 char hex   | true          | the ID of a keyword that MOs matching the `rule` will be routed to    |
| shortCode | 24 char hex   | true          | the ID of the shortcode that the MO route works on    |
| rule      | string (regex expression) | true  | a valid regex rule; MOs to the `shortcode` that match this rule will be considered equivalent to the MO route's `keyword` |

#### v2

##### Parameters
id (optional, 24 char hex) ... the MO Route's unique identifier. Required in PUT & DELETE requests; when omitted from a GET request, returns a collection of all MO Routes.

##### retrieve moroute
```
GET /v2/moroute/{id}
```
##### Response 
```
Status: 200
[MORoute][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### create moroute
```
POST /v2/moroute/{id}
```
##### Request
```
[MORoute][]
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### update moroute
```
PUT /v2/moroute/{id}
```
##### Request
```
[MORoute][]
```
##### Response 
```
Status: 200
[MORoute][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### delete moroute
```
DELETE /v2/moroute/{id}
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

### Role

#### `Role` model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | false | Account ID    |
| createdBy | string    | false | Created by User ID    |
| creationDate  | Date  | false | Creation date |
| group | string    | false | Group ID  |
| groupsVisible | list  | false | Groups visible    |
| id    | string    | false | Object ID |
| name  | string    | false | Role name |
| permissions   | list  | false | Permissions   |
| status    | string    | false | Status    |

#### v1

##### Parameters
id (optional, 24 char hex) ... the role's unique identifier. Required in GET, PUT & DELETE requests.

##### get role
```
GET /v1/role/{id}
```
##### Response 
```
Status: 200
[Role][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### delete role
```
DELETE /v1/role/{id}
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### update role
```
PUT /v1/role/{id}
```
##### Request
```
[Role][]
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### create role
```
POST /v1/role/{id}
```
##### Request
```
[Role][]
```
##### Response 
```
Status: 200
[Role][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

#### v2

##### Parameters
id (optional, 24 char hex) ... the role's unique identifier. Required in GET, PUT & DELETE requests.

##### get role
```
GET /v2/role/{id}
```
##### Response 
```
Status: 200
[Role][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * * 
##### delete role
```
DELETE /v2/role/{id}
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### update role
```
PUT /v2/role/{id}
```
##### Request
```
[Role][]
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### create role
```
POST /v2/role/{id}
```
##### Request
```
[Role][]
```
##### Response 
```
Status: 200
[Role][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

### Reporting

Reporting comes in both synchronous and asynchronous varieties. Synchronous reporting retrieves metrics on your program in JSON format for consumption by a browser or application. Asynchronous reporting lets you create, run and rerun reporting templates that are compiled in the background, retrieving them as CSV files.

#### Synchronous Reporting

These reports use several query parameters in common to determine the scope of the report:

| parameter  | type  | required  | description   |
|-----|-----|-----|-----|
| beginOn       | date  | false | the start time of the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| endOn         | date  | false | the start time of the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| bucketSize    |'DAY', 'WEEK', 'MONTH'     | true | the interval into which reporting data is aggregated |
| size          | integer | false | the number of results to return in the collection; defaults to 20 |
| page          | integer   | false | the page of the collection to return; defaults to 1 |
| summaryType   |CAMPAIGN', 'MOBILEFLOW', 'KEYWORD |  |  |
| timeframe     | 'TODAY', 'YESTERDAY', 'THISWEEK', 'LAST7', 'LASTWEEK', 'LAST14', 'THISMONTH', 'LAST30', 'LASTMONTH', 'ALLTIME' | false | sets the time period covered by the report; either `timeframe` or `beginOn` and `endOn` must be present | 

```
GET /v1/reporting/subscriberGrowthReport?listId={listId}&filterId={filterId}
```

Retrieve subscriber growth report matching filter parameters

##### Parameters
+ listId (optional, 24 char hex) ... the ID of the list whose growth is to be tracked. If both this and `filterId` are omitted, the report will be for all lists.
+ queryFilterId (optional, 24 char hex) ... the ID of the smart list whose growth is to be tracked. If both this and `listId` are omitted, the report will be for all lists.

##### Response 
```
Status: 200
[Collection][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### Export list of subscribers for a specified filtered list
```
GET /v1/reporting/listDetails/export/{id}
```
##### Parameters
id (required, 24 char hex) ... the ID of the list or smart list to be exported

##### Request
```
Accept: application/csv
```
##### Response 
```
Status: 200
Content-Type: application/csv
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### Export subscriber messages on a specified short code. Defaults to session short code.
```
GET /v1/reporting/subProfile/export/{id}
```
##### Parameters
id (required, 24 char hex) ... the ID of the shortcode messages will be exported from
##### Response 
```
Status: 200
[ReportingTemplateResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### Export inbox messages on a specified short code. Defaults to session short code.
```
GET /v1/reporting/inbox/export
```
##### Request
```
[ReportingTemplateRequest][]
```
##### Response 
```
Status: 200
[ReportingTemplateResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
### messageDetailsReport
```
GET /v1/reporting/messageDetails
```
Retrieve message details report matching filter parameters

##### Request
```
[ReportingTemplateRequest][]
```
##### Response 
```
Status: 200
[ReportingTemplateResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
### messageDetailsExport
```
GET /v1/reporting/messageDetails/export
```
Export message details report matching filter parameters
##### Request
```
[ReportingTemplateRequest][]
```
##### Response 
```
Status: 200
[ReportingTemplateResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
### messageSummaryReport
```
GET /v1/reporting/messageReport
```
Retrieve message summary report matching filter parameters
##### Request
```
[ReportingTemplateRequest][]
```
##### Response 
```
Status: 200
[ReportingTemplateResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
### messageSummaryReportExport
```
GET /v1/reporting/messageReport/{summaryObject}/export
```
Export message summary report matching filter parameters

##### Parameters
summaryObject (required, 24 char hex) ... ID of the object being summarized

##### Request
```
[ReportingTemplateRequest][]
```
##### Response 
```
Status: 200
[ReportingTemplateResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
### subscriberGrowthExport
```
GET /v1/reporting/subscriberGrowthReport/export
```
Export subscriber growth report matching filter parameters

##### Request
```
[ReportingTemplateRequest][]
```
##### Response 
```
Status: 200
[ReportingTemplateResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
### messageSummaryActivity
```
GET /v1/reporting/messageReport/activity
```
Retrieve message summary report for session short code

##### Request
```
[ReportingTemplateRequest][]
```
##### Response 
```
Status: 200
[ReportingTemplateResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Staus: 403
```
##### Response 
```
Status: 500
```
* * *
### broadcastSummaryReport
```
GET /v1/reporting/broadcastSummary
```
Retrieve broadcast summary report for session short code

##### Request
```
[ReportingTemplateRequest][]
```
##### Response 
```
Status: 200
[ReportingTemplateResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Staus: 403
```
##### Response 
```
Status: 500
```
* * *
### broadcastSummaryExport
```
GET /v1/reporting/broadcastSummary/export
```
Export broadcast summary report for session short code
##### Request
```
[ReportingTemplateRequest][]
```
##### Response 
```
Status: 200
[ReportingTemplateResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
### Asynchronous Reporting

Asynchronous reporting allows larger and more complext reports to be saved, delegated to a separate reporting server and run without impacting the resources allocated to the application as a whole.

These methods involve the creation and management of _reporting templates_, which contain a set of search parameters defining the report, the running of these templates, which applies the template's parameters to the application's current data to generate a _file_, and the retrieval of those files once the template is finished running.

Reporting data is retrieved as a downloadable CSV file.

#### Reporting Template Models

The following models are used in asynchronous reporting.

##### `ReportingStatus` model

the current state of the reporting server.

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| lag   | number    | true  | Reporting lag in minutes  |
| status    | string    | true  | Reporting service status  |

##### `ReportingTemplateRequest` model

used when submitting requests (GET, POST or PUT) having to do with reporting templates.

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | false | Account ID    |
| group | string    | false | Group ID  |
| id    | string    | false | Object ID |
| name  | string    | false | Name of the report. This name will be used for the csv generated  |
| query  | `ReportingRequestQuery` model | false | Report query details. This is specific to the type of report |
| shortCode | string    | false | Short Code ID |
 
##### `ReportingTemplateResponse` model

represents a reporting template when reutrned from the application

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | true  | Account ID    |
| group | string    | true  | Group ID  |
| id    | string    | true  | Reporting template ID |
| lastReport  | ReportResponse model  | true  | Last run report results
| query  | `ReportingRequestQuery` model | false | Report query details. This is specific to the type of report. See Reporting Query Models, below. |
| shortCode | string    | true  | Short Code ID |

#### Reporting Query Models

The `query` property of a `ReportingTemplateResponse` or `ReportingTemplateRequest` model will be one of the following query models, each reprepsenting a different type of report.

##### Message Details report

a comprehensive report of every message matching the template criteria received and/or sent by the application

| property | type | required | description |
|-----|-----|-----|-----|
| type          | 'messageDetails' | true | denotes a Message Details report |
| messageType   | 'MO', 'MT' | false | the direction of messages included in the report; report will include all messages if absent |
| contentType   | 'SUBSCRIPTION', 'STOP', 'BASICTEXT', 'CATCHALL', 'COLLECTMETADATA', 'TAGMETADATA', 'DYNAMICCONTENT', 'POLL' | false | the type of content included in the report; defaults to all if absent |
| timeframe     | 'TODAY', 'YESTERDAY', 'THISWEEK', 'LAST7', 'LASTWEEK', 'LAST14', 'THISMONTH', 'LAST30', 'LASTMONTH', 'ALLTIME' | false | sets the time period covered by the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| beginOn       | date  | false | the start time of the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| endOn         | date  | false | the end time of the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| campaign      | 24-char hex   | false | the ID of a campaign whose messages are included in the report |
| mobileFlow    | 24-char hex   | false | the ID of a campaign whose messages are included in the report |
| keyword       | 24-char hex   | false | the ID of a campaign whose messages are included in the report |

##### Message Totals report

an report that aggregates numbers of messages by type and interval

| property | type | required | description |
|-----|-----|-----|-----|
| type          | 'messageSummary' | true | denotes a Message Totals report |
| summaryType   |CAMPAIGN', 'MOBILEFLOW', 'KEYWORD |  |  |
| beginOn       | date  | true | the start time of the report | 
| endOn         | date  | true | the end time of the report | 
| bucketSize    |'DAY', 'WEEK', 'MONTH'     | true | the interval into which reporting data is aggregated |

##### Subscriber Growth report

a report showing the change in subscriber status for one or more lists or smart lists over time, aggregated by interval

| property | type | required | description |
|-----|-----|-----|-----|
| type          | 'subscriberGrowth' | true | denotes a Subscriber Growth report |
| lists         |   array   | true | the lists whose activity is tracked in the report |
| timeframe     | 'TODAY', 'YESTERDAY', 'THISWEEK', 'LAST7', 'LASTWEEK', 'LAST14', 'THISMONTH', 'LAST30', 'LASTMONTH', 'ALLTIME' | false | sets the time period covered by the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| beginOn       | date  | false | the start time of the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| endOn         | date  | false | the start time of the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| bucketSize    |'DAY', 'WEEK', 'MONTH'     | true | the interval into which reporting data is aggregated |

##### Broadcast Summary report

a report of all broadcasts sent by the application to one or more lists or filters for a given time period

| property | type | required | description |
|-----|-----|-----|-----|
| type          | 'broadcastSummary' | true | denotes a Broadcast Summary report |
| lists         |   array   | true | the lists whose activity is tracked in the report |
| timeframe     | 'TODAY', 'YESTERDAY', 'THISWEEK', 'LAST7', 'LASTWEEK', 'LAST14', 'THISMONTH', 'LAST30', 'LASTMONTH', 'ALLTIME' | false | sets the time period covered by the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| beginOn       | date  | false | the start time of the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| endOn         | date  | false | the start time of the report; either `timeframe` or `beginOn` and `endOn` must be present | 

##### Poll Results report

a report of poll results gathered through the use of the `interactive poll` flow component

| property | type | required | description |
|-----|-----|-----|-----|
| type          | 'pollSummary' | true | denotes a Poll Results report |
| mobileFlow         |   24-char hex   | false | the ID of a mobile flow containing a poll whose reuslts are summarized in the report. |

##### Parameters
id (optional, 24-char hex) ... the ID of the reporting template

#### Retrieve last run report
```
GET /v2/reporting/{id}
```
Returns the most recent results from a reporting template. Note that the Accept header in this request is application/csv, unlike most requests made to Revere Mobile

##### Request 
```
Accept: application/csv
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
#### Retrieve reporting template information by id
```
GET /v2/reporting/{id}
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
#### Rerun report template
```
PUT /v2/reporting/{id}
```
updates the file associated with a reporting template for retrieval later
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
#### Delete access to a reporting template
```
DELETE /v2/reporting/{id}
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
#### Create a new reporting template
```
POST /v2/reporting/{id}
```
##### Request
```
[ReportingTemplateRequest][]
```
##### Response 
```
Status: 200
[ReportingTemplateResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
```
GET /v2/reporting/
```
##### Response 
```
Status: 200
[Collection][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
#### Retrieve reporting status including lag
``` 
GET /v2/reporting/status
```
##### Response 
```
Status: 200
[ReportingStatus][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

### Shortcode

**`shortcode` model**

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| id             | 24 char hex   | yes   | The ID of the short code |
| provider       | string        | yes   | Name of the aggregator that delivers messages to/from the shortcode |
| countryCode    | integer       | yes   | Country code assocaited with this shortcode; will be 1 in all US/Canadian instances |
| dedicated      | boolean       | yes   | Will be true in all instances |
| description    | string        | yes   | The plan-language name of the shortcode; will be an organization's name unless it is a shared shortcode |
| maxSmsLength   | integer       | yes   | Maximum length of messages on this shortcode; 160 in the US, 136 in Canada |
| profileId      | integer       | yes   | | 
| shortcode      | integer       | yes   | The literal shortcode |
| testPrefix     | string        | no    | |
| defaultStopResponse    | string | no   | The message that will be delivered to users who text STOP and its aliases to the shortcode 
| defaultHelpResponse    | string | no   | The message that will be delivered to users who text STOP and its aliases to the shortcode 
| carrierStopResponses   | object | no   | Object representing different STOP messages that will be delivered to users based on their carrier. Not used generally.
| carrierHelpResponses   | object | no   | Object representing different STOP messages that will be delivered to users based on their carrier. Not used generally.
| status                 | string | yes  | "ACTIVE" or "INACTIVE" |
| forwardURL             | string | no   | Should always be null |
| sessionTimeout         | integer | yes | Time (in milliseconds) that the session window should remain open |
| mms                    | boolean  |   yes | true only for shortcodes enabled for MMS delivery |

```
POST /v1/shortcode/sessionshortcode/{shortcodeId}
```
##### Change your session shortcode

Many platform objects are tied to a specific shortcode as well as a permissions group. Use this method to change the shortcode you are working on in order to access and manipulate these objects. Because most users will have access to only one shortcode, this method will not be necessary to the majority.

#####  Parameters
shortcodeId (required, 24-char hex) ... The ID of the shortcode you are switching to

##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

#### v1

##### Parameters
id (optional, 24 char hex) ... The smart list's unique identifier. Required in GET, PUT & DELETE requests. Whem omitted from a GET request, the request will return a collection of all smart lists.
##### get shortcode
```
GET /v1/shortcode/{id}
```
##### Response 
```
Status: 200
[Shortcode][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

#### v2

##### update shortcode
```
PUT /v2/shortcode/{id}
```
Update certain properties of a shortcode. May only be used to update the following:

* `defaultHelpResponse`
* `defaultStopResponse`
* `sessionTimeout`

##### Request
```
[Shortcode][]
```
##### Response 
```
Status: 200
[Shortcode][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

### Smart Lists

A smart list is similar to a persistent filter, comprised of constituent lists and criteria filters, but which is treated like a subscription list for all intents and purposes, including reporting.

#### `smartlist` model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| id    | 24 char hex   | yes   |  the ID of the smart list; omitted from `create smart list` |
| account    | 24 char hex   | no   |  the ID of the smart list's Revere Mobile account; omitted from `create smart list` |
| group    | 24 char hex   | no   |  the ID of the smart list's permissions group; defaults to the user's default group |
| shortCode    | 24 char hex   | no   | the ID of the smart list's shortcode; defaults to the user's default shortcode  |
| queryFilterDetails    | QueryFilterDetails API model   | yes   |  API model reflecting query criteria for the smart list |
| lists    | array  | yes   |  array of lists to be included in the smart list |
| name    | string   | yes   |  human-friendly name for the smart list |


#### v2

##### Parameters
id (optional, 24 char hex) ... The smart list's unique identifier. Required in GET, PUT & DELETE requests. When omitted from a GET request, the request will return a collection of all smart lists.

##### create smart list
```
POST /v2/smartlist/{id}
```
##### Request
```
[SmartListRequest][]
```
##### Response 
```
Status: 200
[SmartListResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### get smart list
```
GET /v2/smartlist/{id}
```
##### Response 
```
Status: 200
[SmartListResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### delete smart list
```
DELETE /v2/smartlist/{id}
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
#### Share smart list: grant another permissions role access to the smart list.
```
POST /v2/smartlist/{smartlistid}/share/{roleid}
```
##### Parameters
+ smartlistid (24 char hex) ... the ID of the smartlist to be shared.
+ roleid (24 char hex) ... the ID of the permissions role that should receive access to the smart list
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response
```
Status: 403
```
##### Response 
```
Status: 500
```

### Subscriber

Subscribers are the individual members Revere Mobile interacts with.
```
GET /v1/subscriber/{idOrMsisdn}
```
#### Retrieve subscriber by phone number or system ID

##### Parameters
idOrMsisdn (optional, 24 char hex or 12-digit msisdn) ... may be the subscriber's 24-char hex identifier or their mobile phone number.

##### Response 
```
Status: 200
[Subscriber][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
#### Retrieve subscriber by profile metadata
```
GET /v1/subscriber?search={search}
```
**Profile metadata** is a privileged status of metadata fields used to build a core subscriber profile. The following fields are considered profile metadata (note that some permission groups may have their own fields which are meant to store similar qualities as these):

| Profile field | Description |
|-----          |---------------|
| msisdn      |    10 digit msisdn is (ie. 6081112222)  |
| areaCode    |   Three digit area code (ie. 608)   |
| state       |   Abbreviated state (ie. WI)    |
| firstName   |   First name (ie. Jon) |
| lastName    |    Last name (ie. Snow)  |
| email       |   Email address (ie. jsnow@blackwatch.org)    |
| facebook    |    Facebook surname (ie. stark.bastard23)   |
| twitter     | Twitter surname (ie. stark.bastard23)   |
| zipCode     | Five digit zip code (ie. 54806) |   
| timeZone    |    Timezone value (ie. -0700)    |

##### Parameters
search (optional, string) ... search query to match across all of a subscriber's profile metadata.

##### Response 
```
Status: 200
[Subscriber][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
#### Retrieve the number of subscribers in a list or filter.
```
GET /v1/subscriber/count
```
##### Parameters
+ listId (optional, 24 char hex) ... the ID of a list that you are counting subscribers on. Mutually exclusive with `filterId`.
+ filterId (optional, 24 char hex) ... the ID of a filter or smart list that you are counting subscribers on. Mutually exclusive with `listId`.

##### Response 
```
Status: 200
[SubscriberCountCollection][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
#### Retrieve a paginated collection of subscribers belonging to a list or filter.
```
GET /v1/subscriber
```
This method operates differently from other collection-retrieval methods. If retrieving a number of pages, the maximum `size` of each page is 60; passing a number greater than this or passing -1 will result in pages with 60 records each. To retrieve up to 5000 records per request, omit `page` and set `size` to any value up to 5000. Subsequent requests may contain the `lastId` parameter to retrieve following "pages" of subscribers.

##### Parameters
+ listId (optional, 24 char hex) ... the ID of a list for which to return subscribers. Mutually exclusive with `filterId`.
+ filterId (optional, 24 char hex) ... the ID of a filter for which to return subscribers. Mutually exclusive with `listId`.
+ page (optional, integer) ... the 1-based index of the page to return. The default value is 1. Omit this parameter if attempting to retrieve more than 60 results per request.
+ size (optional, integer) ... the number of items that a call to the operation will return. The default value is 20. The maximum value is 60 when `page` is included, or 5000 when paginating using the `lastId` parameter.
+ lastId (optional, 24-char hex) ... including this parameter when `page` is absent will return a collection of the specified `size`, beginning with the first subscriber following the subscriber whose ID is equal to this parameter.

##### Response 
```
Status: 200
[Collection][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
#### Add a value for a metadata field to a subscriber.
```
PUT /v1/subscriber/addMetadata/{idOrMsisdn}
```
##### Parameters
idOrMsisdn (optional, 24 char hex or 12-digit msisdn) ... may be the subscriber's 24-char hex identifier or their mobile phone number.
##### Request
```
[MetadataValue][]
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

#### [v2](/v1/subscriber/{idOrMsisdn}?search={search})

##### Parameters
+ idOrMsisdn (optional, 24 char hex or 12-digit msisdn) ... may be the subscriber's 24-char hex identifier or their mobile phone number with country code.
+ search (optional, string) ... search string to be matched in any of a subscriber's profile metadata. Not used when idOrMsisdn is specified.
* * *
##### Retrieve subscriber profile by ID or Mobile Number
```
GET /v2/subscriber/{idOrMsisdn}
```
###### Parameters
idOrMsisdn (required, 24 char hex or 12-digit msisdn) ... may be the subscriber's 24-char hex identifier or their mobile phone number.

##### Response 
```
Status: 200
[Subscriber][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
Adds a subscriber to a subscription list. **Caution: subscribing people using this method does not ensure they have been properly opted-in or welcomed to the program.** Use this method only to add an existing, legitimate subscriber to a different list, not to introduce new people to a list.
```
PUT /v2/subscriber/{idOrMsisdn}/list/{listId}
```
##### Parameters
+ idOrMsisdn (required, 24 char hex or 12-digit msisdn) ... may be the subscriber's 24-char hex identifier or their mobile phone number.
+ listId (required, 24 char hex or 12-digit msisdn) ... the ID of a subscription list the subscriber will be added to.
  
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
Retrieve a collection of subscribers matching the listId and/or filterId criteria. This method operates unlike other collection methods in that it returns a maximum of 60 results per page if the `size` parameter is either -1, 60 or greater.
```
GET /v2/subscriber?listId={listId}&filterId={filterId}
```
##### Parameters
+ listId (optional, 24 char hex) ... ID of the list whose count you are retrieving.
+ filterId (optional, 24 char hex) ... Id of the filter or smart list whose count you are retrieving.
  
##### Response
```
Status: 200
[Collection][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
Retrieve messages sent to and from a subscriber, with delivery status (if known)
```
GET /v2/subscriber/{msisdn}/messages
```
##### Parameters
msisdn (required, 12-digit msisdn) ... the subscriber's mobile phone number

##### Response 
```
Status: 200
[SubscriberMessagesResponse][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

### Blacklist
The blacklist is a collection of subscribers who the current shortcode is prevented from interacting with. No response will be made to any inbound messages from these subscribers and no outbound messages will ever be delivered to them. 

#### v2

##### Parameters
+ idOrMsisdn (required, 24 char hex or 12-digit msisdn) ... may be a subscriber's 24-char hex identifier or their mobile phone number; omitted from the _Retrieve blacklist_ method
+ shortCode (optional, 24 char hex or 12-digit msisdn) ... the shortcode to blacklist the subscriber on; defaults to the session shortcode if omitted

##### Add subscriber to blacklist
```
POST /v2/subscriber/blacklist/{idOrMsisdn}?shortCode={shortCode}
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### Remove subscriber from blacklist
```
DELETE /v2/subscriber/blacklist/{idOrMsisdn}?shortCode={shortCode}
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### Retrieve blacklist
```
GET /v2/subscriber/blacklist/{idOrMsisdn}?shortCode={shortCode}
```
##### Response 
```
Status: 200
[Collection][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

### Trigger

A trigger is a platform object that can cause a message to be sent. In plain language, both broadcasts and keywords are triggers. Both can be accessed via this API endpoint, though the use of the Trigger API for broadcasts is deprecated in favor of the Broadcast API.

#####`Trigger` Model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | false | Account ID    |
| creationDate  | Date  | false | Creation date |
| group | string    | false | Group ID  |
| mobileFlow    | string    | false | Mobile flow ID    |
| name  | string    | false | Trigger name  |
| shortCode | string    | false | Short code ID |

#### v1

##### Parameters
id (optional, 24 char hex) ... the trigger's unique identifier. Required in PUT & DELETE requests, and in GET requests to retrieve information about a specific trigger.

##### get trigger by id
```
GET /v1/trigger/{id}
```
Retrieve information on a specific trigger. When passed without the {id} parameter, this retrieves a paginated collection of all triggers.

##### Response 
```
Status: 200
[Trigger][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### delete trigger
```
DELETE /v1/trigger/{id}
```
Remove a keyword or scheduled broadcast. The {id} parameter is required.

##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### update trigger
```
PUT /v1/trigger/{id}
```
Reassign a keyword to a different mobile flow, or unassign it entirely.

##### Request
```
[Trigger][]
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### create trigger
```
POST /v1/trigger/{id}
```
Create a new keyword.

##### Request
```
[Trigger][]
```
##### Response 
```
Status: 200
[Trigger][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### Retrieve a collection of recent broadcasts by pagination parameters.
```
GET /v1/trigger/recent
```
##### Response 
```
Status: 200
[Collection][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### Check to see whether a given keyword is available on the current shortcode.
```
GET /v1/trigger/isKeywordAvailable/{name}
```
##### Parameters
name (required, string) ... the keyword to check for availability
##### Response 
```
Status: 200
[Collection][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### Retrieve a list of scheduled broadcasts by pagination parameters.
```
GET /v1/trigger/broadcast
```
##### Response 
```
Status: 200
[Collection][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

### User

Use these endpoints to control other users' access to Revere Mobile.

##### `User` Model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | false | Account ID    |
| apiKey    | string    | false | API Key   |
| createdBy | string    | false | Created by User ID    |
| defaultShortCode  | string    | false | Default short code    |
| details   | `UserDetails` Model   | false | User details  |
| group | string    | false | Group ID  |
| id    | string    | false | Object ID |
| name  | string    | false | User name |
| password  | string    | false | Password  |
| role  | string    | false | Role ID   |
| shortCodes    | list  | false | Short codes   |
| status    | string    | false | Status    |

**`UserDetails` Model**

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| company   | string    | false | Company   |
| email | string    | false | Email address |
| lastLogin | Date  | false | Last login date   |
| mobile    | string    | false | Mobile number |
| name  | string    | false | Name  |
| phone | string    | false | Phone number  |
| title | string    | false | Title |

#### v1

##### Parameters
id (optional, 24 char hex) ... the user's unique identifier. Required in PUT & DELETE requests, and in GET requests to retrieve information about a specific trigger.

#### get user
```
GET /v1/user/{id}
```
Retrieve information on a specific user with the {id} parameter set, or retrieve a collection of all users without {id}

##### Response 
```
Status: 200
[User][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * * 
##### delete user
```
DELETE /v1/user/{id}
```
Remove a user from the Revere Mobile platform

##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### update user
```
PUT /v1/user/{id}
```
Change a user's properties

##### Request
```
[User][]
```
##### Response 
```
Status: 204
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
##### create user
```
POST /v1/user/{id}
```
Create a new user

##### Request
```
[User][]
```
##### Response 200
```
[User][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```
* * *
Create or reset a user's API key. The user may use this key to authenticate API requests as described in Authentication, above. A note of caution: once created, an API key may not be retrieved, only reset.
```
POST /v2/user/{id}/apikey
```
##### Parameters
id (optional, 24 char hex) ... the ID of the user you need to create an API key for.

##### Request
```
Accept: application/json
```  
##### Response 
```
200
[APIKey][]
```
##### Response 
```
Status: 400
```
##### Response 
```
Status: 401
```
##### Response 
```
Status: 403
```
##### Response 
```
Status: 500
```

### Mobile Flow Components

A mobile flow represents a complex interaction with a subscriber or other end-user. A mobile flow is composed of a series of content modules that contain the specifics of the interaction. You can set the maximum number of messages per month that the mobile flow will send to any one subscriber.

Keywords can be assigned to a mobile flow. When a subscriber texts to a keyword, all mobile flows that are associated with that keyword are triggered for the subscriber. If no keywords are assigned to a mobile flow, that mobile flow is inactive.

A mobile flow can be assigned to a campaign. Campaigns are used to group business objects and aggregate information for reports.

| Content module type | Description |
|-----                |------       |
| BASICTEXT           | Sends a text message to the subscriber.
| COLLECTMETADATA     | Prompts the subscriber for the value of a metadata field.
| DYNAMICCONTENT      | Posts information to a web service and proceeds based on the response back from that service.
| POLL                | Prompts the subscriber to participate in a poll and branches the flow based on the poll answer.
| POSTTOURL           | Posts information to a web service.
| SUBSCRIPTION        | Adds the subscriber to a list.
| TAGMETADATA         | Assigns a value for the subscriber to a metadata field.
| VALIDATION          | Branches the flow based on validation factors.

Many of the modules contain fields for message text that is sent to the subscriber. Message fields support all standard GSM characters. Use the following guidelines for any parameter values that contain a message for a subscriber.

Avoid the use of curly braces, double quotes, and carriage returns to maintain valid JSON.
Include the protocol name, such as http:// or mailto: as part of any URL.
The following sections describe each of the available content module types.

#### BASICTEXT

A basic text content module sends a text message to a subscriber.

This module is defined by the following parameters.

Parameter    |    Description
|----|----|
response    |    The text to send to the subscriber.

#### COLLECTMETADATA

A collect metadata module prompts the subscriber for the value for a metadata field.

The content module first sends a request message that prompts the subscriber for the metadata value. If the response is a valid value, as defined by the metadata field, the modules sends a response message is sent; otherwise, it sends an invalid format message which should prompt the subscriber to resubmit.

This module is defined by the following parameters.

Parameter    |    Description
|----|----|
invalidFormatMessage    |    The response message for an invalid value.
metadataId    |    The ID of the metadata field for which to collect information.
requestMessage    |    The request message for the metadata value.
responseMessage    |    The response message for a valid value.

#### DYNAMICCONTENT

A dynamic content module posts information about the subscriber or interaction to a web service and proceeds based on the response back from that service. The module waits for a response from the web service to determine how to respond to the subscriber.

The web service should respond with a simple XML or JSON payload depending on which format is specified in the URL:

##### XML Payload
```
<dynamiccontent>
    <endSession>true</endSession>
    <response>response text</response>
</dynamiccontent>
```

##### JSON Payload
``` 
{
    "endSession": true,
    "response": "response text"
}
```
The `endSession` value indicates whether to keep the session open for further interaction. If `endSession` is false, further responses from the subscriber will be processed by the same web service; otherwise, further responses will be sent to the next content module in the mobile flow.

The `response` value contains the response message for the subscriber. If `response` is empty, the module does not send a response message to the subscriber.

This module is defined by the following parameters.

Parameter    |    Description
|----|----|
url    |    The URL of the target web service.
The URL of the target web service can contain the following substitution strings.

Substitution    |    Description
|----|----|
$carrier    |    The carrier of the subscriber.
$keyword_id    |    The ID of the keyword used by the subscriber.
$keyword_name    |    The name of the keyword used by the subscriber.
$mobile_text    |    The text that the user entered.
$msisdn    |    The domestic or international MSISDN of the subscriber.
$short_code    |    The short code of the mobile flow.
When the module calls the web service, it includes in the POST payload information for all of the above data. If the target URL contains a format query parameter set to 'json', then the POST payload is formatted as JSON; otherwise, the POST payload is formatted as XML.

#### POLL

A poll content module involves the subscriber in a poll. This module can branch based on the subscriber's choice.

Each choice has the format, value: description, where value and description are provided in each choice object.

This module is defined by the following parameters.

Parameter    |    Description
|----|----|
allowMultipleVotes    |    true to allow a subscriber to cast multiple votes; otherwise, false.
choices    |    An array of choice objects that represent the options on which to vote.
pollQuestion    |    The message that contains the poll question.
pollResults true to send the current results to the subscriber after they vote.
response    |    The message to send the subscriber after they vote.
sendResults    |    true to attach the current poll results to the poll question; otherwise, false.
Each choice object is defined by the following parameters.

Parameter    |    Description
|----|----|
description |The descriptive text for the choice.
message |The message to send the subscriber if they pick this choice.
mobileFlow    |    The ID of the mobile flow to which to branch if nextStep is 'forwardToMobileFlow'.
nextStep    |    Either 'proceed', 'terminate', or 'forwardToMobileFlow'. This indicates the next step the mobile flow takes if the subscriber picks this choice. Specify 'proceed' to have the flow proceed to the next module in the flow. Specify 'terminate' to exit the mobile flow. Specify 'forwardToMobileFlow' to branch to the flow indicated by the mobileFlowb parameter.
value    |    The symbol that the subscriber enters to pick this choice.

#### POSTTOURL

A post to URL module posts information about the subscriber or interaction to a web service.

This module is defined by the following parameters.

Parameter    |    Description
|----|----|
url |The URL of the target web service.
The URL of the target web service can contain the following substitution strings.

Substitution    |    Description
|-----|------|
$carrier    |    The carrier of the subscriber.
$keyword_id |    The ID of the keyword used by the subscriber.
$keyword_name    |    The name of the keyword used by the subscriber.
$mobile_text    |    The text that the user entered.
$msisdn |    The domestic or international MSISDN of the subscriber.
$short_code |    The short code of the mobile flow.
When the module calls the web service, it includes in the POST payload information for all of the above data. If the target URL contains a format query parameter set to 'json', then the POST payload is formatted as JSON; otherwise, the POST payload is formatted as XML.

#### SUBSCRIPTION

A subscription content module adds a subscriber to a list, with an optional confirmation dialog.

This module is defined by the following parameters.

Parameter    |    Description
|----|----|
confirmMessage    |    Optional. The confirmation message sent when the subscriber is successfully added to the list.
listId    |    The ID of the list to which this module adds a subscriber.
optInMessage    |    The second opt in message that asks the subscriber to confirm that they agree to join the list.
optInType    |    Either singleOptIn or doubleOptIn.
subscribedMessage    |    Optional. The message sent when the subscriber is already a member of the list.
For single opt in, the optInMessage parameter is unused. For double opt in, the optInMessage parameter must be specified with the messaging intended to confirm the subscriber’s intent to be added to the list in question.

#### TAGMETADATA

A tag metadata content module assigns a value to a metadata field for the subscriber.

This module is defined by the following parameters. The ID of the metadata field to update is used as the parameter name.

Parameter    |    Description
|----|----|
metadataId    |    The value to assign to the metadata field for the subscriber.

#### VALIDATION

The validation content module can HOST: https://mobile.reverehq.com/apibranch the current flow based on validation factors. If the subscriber passes the validation, the mobile flow progresses based on the `consequentNextStep` and `consequentMobileFlow` parameters; otherwise the flow progresses based on the `alternativeNextStep` and `alternativeMobileFlow` parameters.

The next step parameters can contain either 'proceed', 'terminate', or 'forwardToMobileFlow'. This indicates that the associated next step the mobile flow should take. Specify 'proceed' to have the flow proceed to the next module in the flow. Specify 'terminate' to exit the mobile flow. Specify 'forwardToMobileFlow' to branch to the flow indicated by the associated mobile flow parameter.

The validation factors are represented as a set of Boolean conditions, and the outerOperator indicates how to aggregate the results.

This module is defined by the following parameters.

Parameter    |    Description
|----|----|
alternativeMobileFlow    |    The ID of the mobile flow to which to branch if validation fails and alternativeNextStep is 'forwardToMobileFlow'.
alternativeNextStep |Either 'proceed', 'terminate', or 'forwardToMobileFlow'.
alternativeResponse |The message to send if the subscriber fails the validation.
conditions    |    An array of condition objects.
consequentMobileFlow    |    The ID of the mobile flow to which to branch if validation succeeds and consequentNextStep is 'forwardToMobileFlow'.
consequentNextStep    |    Either 'proceed', 'terminate', or 'forwardToMobileFlow'.
consequentResponse    |    The message to send if the subscriber passes the validation.
outerOperator    |    Either 'any' or 'all'. Specify 'any' to pass validation if any of the conditions evaluates to true. Specify 'all' to pass validation only if all of the conditions evaluate to true.
The innerOperator |indicates how the other parameters are interpreted.

* 'in' checks whether the subscriber is on a list.
* 'nin' checks whether the subscriber is not on a list.
* 'has' checks whether a value is assigned to a metadata field for the subscriber.
* 'doesNotHave' checks whether no value is assigned to a metadata field for the subscriber.
* 'hasValue' checks whether a metadata field for the subscriber contains a specific value. If the metadata field contains multiple values, this returns true if any of the field's values matches the rightHandValue parameter.
* 'doesNotHaveValue' checks whether a metadata field for the subscriber does not contain a specific value. If the metadata field contains multiple values, this returns true if none of the field's values matches the rightHandValue parameter.
Each condition object is defined by the following parameters.

Parameter    |    Description
|----|----|
innerOperator    |    Either 'in', 'nin', 'has', 'doesNotHave', 'hasValue', or 'doesNotHaveValue'.
leftHand    |    Always 'subscriber'.
rightHand    |    The ID of the list or the ID of the metadata field, depending on the value of the innerOperator parameter.
rightHandValue    |    The value to check, for the 'hasValue' and 'doesNotHaveValue' operators.

### Examples

The Revere Mobile platform uses a REST architecture. All requests to the platform must set the Content-Type and Accept HTTP headers to application/json. While the platform can accept calls over the HTTP or HTTPS protocol, by default, you should use the HTTPS protocol. When you authenticate a session, the response will set two cookies: SessionId and JSESSIONID. You must include these cookies in all subsequent requests, they identify your authenticated session. All the examples below include HTTP headers and payload for requests and responses as given by curl.

#### Example 1: Logging in and out

##### To authenticate a session

To start an authenticated session, call the v1/authenticate method, using the username and password associated with your account.

Send a POST request to https://revolutionmsg.com/v1/authenticate. The JSON request payload has the following format, where username and password are your username and password.

##### HTTP Request:
```
    POST /v1/authenticate/ HTTP/1.1
    User-Agent: curl/7.30.0
    Host: revolutionmsg.com
    Content-Type:application/json
    Accept:application/json
    Content-Length: 48
    {
      "username" : "YOUR_USERNAME_HERE", 
      "password" : "YOUR_PASSWORD_HERE"
            }
```

##### HTTP Response:
```
    HTTP/1.1 200 OK
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Methods: GET, POST, DELETE, PUT
    Access-Control-Allow-Headers: Content-Type
    Set-Cookie: JSESSIONID=c078dc10-6b67-4fbb-9295-b53e1c1525fa; Path=/; HttpOnly
    Set-Cookie: rememberMe=deleteMe; Path=/; Max-Age=0; Expires=Tue, 20-May-2014 20:30:59 GMT
    Set-Cookie: SessionId=c078dc10-6b67-4fbb-9295-b53e1c1525fa;Version=1;Path=/api
    Content-Type: application/json
    Transfer-Encoding: chunked
    Server: Jetty(7.4.5.v20110725)
```  
On successful authentication, the response has a status code of 200 (OK), a null payload, and the response sets the SessionId and JSESSIONID cookies, which identifies your session.

##### To check session status

Your session remains authenticated for up to 30 minutes of idle time. You can call the v1/authenticate/whoami method to check the current session status.

Send a GET request to https://revolutionmsg.com/v1/authenticate/whoami
If your session is still authenticated, the response has a status code of 200 (OK), and the response payload contains information about your session.

##### HTTP Request:
```
    GET /v1/authenticate/whoami HTTP/1.1
    User-Agent: curl/7.30.0
    Host: revolutionmsg.com
    Cookie: SessionId=0d9f43c7-dee6-4297-b555-c25f13b496b2; JSESSIONID=0d9f43c7-dee6-4297-b555-c25f13b496b2
    Accept:application/json
```
##### HTTP Response:
```
    HTTP/1.1 200 OK
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Methods: GET, POST, DELETE, PUT
    Access-Control-Allow-Headers: Content-Type
    Content-Type: application/json
    Transfer-Encoding: chunked
    Server: Jetty(7.4.5.v20110725)

    {
      "impersonated": false,
      "username": "charlie",
      "account": "5e7fa7166a465eefd78fb5ee",
      "group": "5e6fa6177a475eefd68fb5f1",
      "role": "5e7fa7186a475eefd78fb5f8",
      "permissions": [
        ...
      ],
      "isRoot": false,
      "isAdmin": false,
      "isGroupAdmin": false
            }
```
Otherwise, the response has a status code of 401 (Unauthorized).

##### To actively close a session

Whenever you are finished accessing the platform, you should actively log out.

Send a POST request with null payload to https://revolutionmsg.com/v1/authenticate/logout
#### Example 2: Sending an SMS message

You can send a simple, one-off message to a subscriber by using the v2/message method.

Start with an authenticated session, as described in the Example 1: Logging in and out section.
Send a POST request to https://revolutionmsg.com/api/v2/message. Include a JSON request payload with the following format, where number is the mobile number to which to send the message, and message is the message to send.

##### HTTP Request
```
    POST /api/v2/message HTTP/1.1
    User-Agent: curl/7.30.0
    Host: revolutionmsg.com
    Cookie: SessionId=ee2fdf0a-96ae-43d1-8315-74626215adbd; JSESSIONID=ee2fdf0a-96ae-43d1-8315-74626215adbd
    Content-Type:application/json
    Accept:application/json
    Content-Length: 67  

    {
      "mobilePhoneNo" : "2025551212", 
      "message" : "Hello, world!" 
    }
```
##### HTTP Response
```
    HTTP/1.1 200 OK
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Methods: GET, POST, DELETE, PUT
    Access-Control-Allow-Headers: Content-Type
    Content-Type: application/json
    Transfer-Encoding: chunked
    Server: Jetty(7.4.5.v20110725) 

    {
      "status": "QUE",
      "id": "53023c6f0cf2eeecfb1bbc0a",
      "account": "5e7fa7166a465eefd78fb5ee",
      "group": "5e6fa6177a475eefd68fb5f1",
      "shortCode": "53012d6b30042ef5572d9a2b",
      "mobilePhoneNo": "12024561414",
      "message": "Hello, world!",
      "subject": null,
      "files": []
    }
```  
#### Example 3: Subscribe an end user to a list and add metadata for the user

This example demonstrates how to create a list and metadata field, join a subscriber to that list and update the metadata field for that subscriber, and then verify the operation by getting the profile of the subscriber.

Start with an authenticated session, as described in the Example 1: Logging in and out section.
Send a POST request to https://revolutionmsg.com/v1/list to create a list to which to add the subscriber. Make a note of the list ID, which is contained in the response payload.

##### HTTP Request
```
    POST /v1/list HTTP/1.1
    User-Agent: curl/7.30.0
    Host: revolutionmsg.com
    Cookie: SessionId=ee2fdf0a-96ae-43d1-8315-74626215adbd; JSESSIONID=ee2fdf0a-96ae-43d1-8315-74626215adbd
    Content-Type:application/json
    Accept:application/json
    Content-Length: 29

    { 
      "name" : "My New List"
    }
```
##### HTTP Response
```
    HTTP/1.1 201 Created
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Methods: GET, POST, DELETE, PUT
    Access-Control-Allow-Headers: Content-Type
    Location: http://revolutionmsg.com/v1/list/53023a0e300445356466e8f3
    Content-Type: application/json
    Transfer-Encoding: chunked
    Server: Jetty(7.4.5.v20110725) 

    {
      "status": "ACTIVE",
      "noOfSubscribers": 0,
      "name": "My New List",
      "shortCode": "53012d6b30042ef5572d9a2b",
      "group": "5e6fa6177a475eefd68fb5f1",
      "account": "5e7fa7166a465eefd78fb5ee",
      "id": "53023a0e300445356466e8f3"
    }
```
Send a POST request to https://revolutionmsg.com/v1/metadata to create the metadata field. Make a note of the metadata ID, which is contained in the response payload.
##### HTTP Request
```
    POST /v1/metadata HTTP/1.1
    User-Agent: curl/7.30.0
    Host: revolutionmsg.com
    Cookie: SessionId=ee2fdf0a-96ae-43d1-8315-74626215adbd; JSESSIONID=ee2fdf0a-96ae-43d1-8315-74626215adbd
    Content-Type:application/json
    Accept:application/json
    Content-Length: 91

    {
      "name" : "My New Metadata",
      "format" : "[a-zA-Z0-9]{1,100}",
      "multiValue" : false
    }
```
##### HTTP Response
```
    HTTP/1.1 201 Created
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Methods: GET, POST, DELETE, PUT
    Access-Control-Allow-Headers: Content-Type
    Location: http://revolutionmsg.com/v1/list/53023e8e0cf2eeecfb1bbe68
    Content-Type: application/json
    Transfer-Encoding: chunked
    Server: Jetty(7.4.5.v20110725) 

    {
      "status": "ACTIVE",
      "eventUrl": null,
      "id": "53023e8e0cf2eeecfb1bbe68",
      "account": "5e7fa7166a465eefd78fb5ee",
      "group": "5e6fa6177a475eefd68fb5f1",
      "format": "[a-zA-Z0-9]{1,100}",
      "name": "My New Metadata",
      "scope": "ACCOUNT",
      "multiValue": false,
      "validValues": null
    }          
```  
Send a POST request to https://revolutionmsg.com/v1/messaging/sendContent endpoint to send a sequence of content modules to the subscriber. The first module will add the subscriber to the list created in step 2. The second module will update the value of the metadata field you created in step 3. In the request payload, update the appropriate fields with the IDs from previous steps.
* Set `msisdns` to the phone number(s) of the subscriber(s) you wish to add to your list.
* Set `listId` to the ID of the list from step 2.
* Set `subscribedMessage` to the message to send the subscriber if they are already a member of the list. This element can be omitted if you do not want to send a message.
* Set `confirmedMessage` to the message to send the subscriber if they are successfully added to the list. This element can be omitted if you do not want to send a confirmation message.
* Set `metadataFieldId` to the ID of the metadata field from step 3.
* Replace My Tag with the value to assign to this field for this subscriber.

##### HTTP Request
```
    POST /v1/broadcast/sendContent HTTP/1.1
    User-Agent: curl/7.30.0
    Host: revolutionmsg.com
    Cookie: SessionId=ee2fdf0a-96ae-43d1-8315-74626215adbd; JSESSIONID=ee2fdf0a-96ae-43d1-8315-74626215adbd
    Content-Type:application/json
    Accept:application/json
    Content-Length: 624

    {
      "msisdns": [
        "12024561414"
      ],
      "modules":[
        {
          "type": "SUBSCRIPTION",
          "params": {
            "listId": "53023a0e300445356466e8f3",
            "optInType": "doubleOptIn",
            "optInMessage": "Would you like to join my mobile list? Text STOP to end, HELP for info. 4 msg/mo. Msg&Data Rates May Apply. More: rm.to/tclegal",
            "confirmMessage": "Thanks for joining my list!",
            "subscribedMessage": "Thanks for your support, you're already subscribed!"
            }
            },
        {
          "type": "TAGMETADATA",
          "params": {
            "53023e8e0cf2eeecfb1bbe68": "My Tag"
            }
            }
      ]
            }
```  
##### HTTP Response
```
    HTTP/1.1 200 OK
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Methods: GET, POST, DELETE, PUT
    Access-Control-Allow-Headers: Content-Type
    Set-Cookie: JSESSIONID=c078dc10-6b67-4fbb-9295-b53e1c1525fa; Path=/; HttpOnly
    Set-Cookie: rememberMe=deleteMe; Path=/; Max-Age=0; Expires=Tue, 20-May-2014 20:30:59 GMT
    Set-Cookie: SessionId=c078dc10-6b67-4fbb-9295-b53e1c1525fa;Version=1;Path=/api
    Content-Type: application/json
    Transfer-Encoding: chunked
    Server: Jetty(7.4.5.v20110725)  
```  
The subscriber receives the confirmed or subscribed message from the short code associated with the session from which the message was initiated.

Send a GET request to https://revolutionmsg.com/v1/subscriber/{id_or_msisdn} endpoint to verify that the subscriber is joined to the list and their metadata field has been updated. Replace the {id_or_msisdn} PATH parameter with the mobile phone number of the subscriber for which you wish to retrieve data.

##### HTTP Request
```
    POST /v1/subsriber/12024561414 HTTP/1.1
    User-Agent: curl/7.30.0
    Host: revolutionmsg.com
    Cookie: SessionId=ee2fdf0a-96ae-43d1-8315-74626215adbd; JSESSIONID=ee2fdf0a-96ae-43d1-8315-74626215adbd
    Content-Type:application/json
    Accept:application/json
    Content-Length: 0  
```  
##### HTTP Response
```
    HTTP/1.1 200 OK
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Methods: GET, POST, DELETE, PUT
    Access-Control-Allow-Headers: Content-Type
    Set-Cookie: JSESSIONID=c078dc10-6b67-4fbb-9295-b53e1c1525fa; Path=/; HttpOnly
    Set-Cookie: rememberMe=deleteMe; Path=/; Max-Age=0; Expires=Tue, 20-May-2014 20:30:59 GMT
    Set-Cookie: SessionId=c078dc10-6b67-4fbb-9295-b53e1c1525fa;Version=1;Path=/api
    Content-Type: application/json
    Transfer-Encoding: chunked
    Server: Jetty(7.4.5.v20110725)  

    {
      "blacklist": [],
      "listDetails": {
        "53023a0e300445356466e8f3" : {
          "details" : {
            mobileFlow : "51c1d70c0cf2872207e46963",
            trigger : "51c1d70c0cf2872207e46964"
            },
          "joinDate" : "Wed Jun 19 13:22:48 CDT 2013"
            }
            },
      "subscriberMetaData": {
        "4ec0a3dd0364de64869d93c3": [
          "DC"
        ],
        "4ec0a3dd0364de64869d93c4": [
          "Eastern"
        ],
        "512a3aff0cf2502eb7ef9e70": [
          "202"
        ],
        "4ec0a3dc0364de64869d93c2": [
          "0012024561414"
        ],
        "53023e8e0cf2eeecfb1bbe68": [
          "My Tag"
        ]
            },
      "mobilePhoneNo": "0012024561414",
      "id": "5e7fabce0cf2658c40c1af7b"
            }
```
