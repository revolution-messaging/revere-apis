# Revere Mobile

HOST: https://mobile.reverehq.com/api

## Introduction

The Revere Mobile platform is a REST service that provides access to the Revere Mobile platform and enables rich, user-oriented web and mobile applications.

The platform allows you to define mobile flows, which can be thought of as a conversation that can be had with a subscriber.

With the platform, you can also define metadata fields that can be associated with and store information about a subscriber. You can define lists to help you manage subscribers and interactions with those subscribers, group mobile flows in campaigns, and generate reports about your subscribers and activity.

Mobile flows offer a rich set of options for interacting with a subscriber. More information about mobile flows in the Flow Components section.

## Reference
## Basic Concepts

### Object IDs

The Revere Mobile service describes many types of objects, such as users, subscribers, lists, metadata files, and mobile flows. The service uses 24-digit hexadecimal string to identify objects, for example, "4e7b79780cf25110e4ee41ac".

### Authentication

There are two ways to authenticate calls to the Revere Mobile platform: authenticate the session, or authenticate each request.

#### Authenticating the session

To authenticate a session, send a POST request to the v1/authentication endpoint. The JSON request contains the user name and password. When you authenticate the session, the service sets SessionId and JSESSIONID cookies, and subsequent calls to the service are authenticated and associated with the user who logged in.

The session ID and the authentication expire after 30 minutes of idle time. To manually log out of the session, send a POST request to the v1/authentication/logout endpoint. For security reasons, you should explicitly logout when your task is complete, rather than relying on a session timeout.

For details on the log in and log out requests, see the Authentication API reference section.

#### Authenticating each request

To separately authenticate each request, include the API key for the user in the Authorization HTTP header. This approach does not require an active session ID. This method is more appropriate for integrations that always use the same credentials and do not want to add the complexity of session logic.

#### Choosing an approach

Whereas all users of the web application will need a user name and password, only users who access the Revere Mobile API would need an individual API key. Your account manager at Revolution Messaging can help you determine which procedure works best for you and will issue an API key if appropriate.

### Session Shortcode

Many platform objects are tied to a shortcode in addition to their permissions group. If you have access to more than one shortcode under your user credentials, the system will assume you are operating on your default shortcode unless you change it with the _Change your session shortcode_ method (see the section on the _shortcode_ endpoint for details). The majority of users will have access to only one shortcode and can safely disregard this requirement.

### HTTP Headers

There are a few HTTP headers that need to be included in all requests. Some have been identified above. If using an authenticated session, there are two cookies that must be included in each subsequent request:

    Cookie: SessionId=0d9f43c7-dee6-4297-b555-c25f13b496b2
    JSESSIONID=0d9f43c7-dee6-4297-b555-c25f13b496b2

If using an API key, the Authorization header must be included instead:

    Authorization: YOUR_APIKEY_HERE

In addition to HTTP headers required for authentication, there are additional ones used to define the format of data being passed back and forth. All of the Revere Mobile platform's APIs use JSON as the payload format. As such, the following headers should be included in all API requests:

    Accept: application/json
    Content-Type: application/json
    
There are a few exceptions to these format headers, those will be identified in the documentation for the specific APIs affected.

### Collections and Pagination

The Revere Mobile API uses pagination to chunk collections of items. A page is simply a range of items from the collection. You may want to retrieve the collection items a page at a time for bandwidth issues, or to relate the request to the UI of an app that only shows a certain number of items per logic page.

In the URL query parameters, you specify the page size and the page number. The size determines how many items are in the returned collection, and the page number determines which page of items is in the returned collection.

For example, if you requested the third page of 20 items, the method would return the 41st through 60th items. If the collection of items on the server contained fewer than 60 items, but more than 40, this same request would return the 41st and all remaining items in the collection. If the collection on the server contained fewer than 41 elements, then this same call would return an empty collection.

#### Request query parameters

* `size` (page size) is the number of items that a call to the operation will return. The default value is -1, which returns all of the items in the collection.
* `page` (page number) is the 1-based index of the page to return. The default value is 1.

For example, the request URL to retrieve the third page of 20 lists would be:
    http://revolutionmsg.com/v1/list?size=20&page=3
#### Response JSON elements
* `page` indicates the 1-based index for this page of items.
* `size` indicates how many items are on each page.
* `total` indicates how many items are in the collection on the server.
* `collection` is an array that contains the items on the requested page.

For the preceding request, if 73 lists are defined, the JSON response would contain the following, where the collection array contains objects describing the requested lists:
```
{
    "page": 3,
    "size": 20,
    "total": 73,
    "collection": [
        ...
    ]
}
```

#### [BroadcastResponse](/APIModel/BroadcastResponse)
**Model**
APIModel for BroadcastResponse
```
{
    "account": "546239d10cf25fdcf0aea9b2",
    "content": "",
    "group":"54623a230cf25fdcf0aeaa5c",
    "id": "5493568f0cf2fcad2e35ecb5",
    "schedule": ""
}
```
#### [BroadcastRequest](/APIModel/BroadcastRequest)
**Model**
APIModel for BroadcastResponse
```
{
    "sendAt": "2015-03-11T17:58:28.367Z",
    "metadata": "4ec0a3dc0364de64869d93c2",
    "content": [
        {
            "channel": "sms",
            "audience": [
                "550081f80cf2dcf7e469337f"
            ],
            "slices": [
                {
                    "percentage": 50,
                    "message": "test",
                    "value": "blah"
                },
                {
                    "percentage": 50,
                    "mobileFlow": "523373030cf2431ec692c57d",
                    "value": "blah1"
                }
            ]
        }
    ]
}
```
#### [APIKey](/APIModel/APIKey)
**Model**
API Model for APIKey
```
{
    "apiKey":"2baa7764-f2fa-4b07-b5de-867dd8ee2532"
}
```
#### [BroadcastSummaryReportQuery](/APIModel/BroadcastSummaryReportQuery)
**Model**
APIModel for BroadcastSummaryReportQuery
```
{
    "id": null,
    "account": null,
    "group": null,
    "shortCode": null,
    "name": null,
    "lastReport": null,
    "query": {
        "type": "broadcastSummary",
        "lists": [
            "54cffeca0cf2c7c3bf30a289",
            "54d001740cf2c7c3bf30a6e4"
        ],
        "beginOn": "2015-01-01",
        "endOn": "2015-01-21"
    }
}
```
#### [MORoute](/APIModel/MORoute)
**Model**
```
{
    "id": "50d4cdec0364ad1a2c78a078",
    "keyword": "4e8d38cf0364b418446ce746",
    "shortCode": "4e8b4b5afda5efeeec370e8a",
    "rule": "^cancel\\s.*"
}
```
#### [SubscriberGrowthReportQuery](/APIModel/SubscriberGrowthReportQuery)
**Model**
APIModel for SubscriberGrowthReportQuery
```
{
    "type": "subscriberGrowth",
    "lists": [
        "50465ac30cf2806788a960af"
    ],
    "beginOn": "2015-01-01",
    "endOn": "2015-01-21",
    "bucketSize": "DAY"
}
```
#### [MessageSummaryReportQuery](/APIModel/MessageSummaryReportQuery)
**Model**
APIModel for MessageSummaryReportQuery
```
{
    "type": "messageSummary",
    "summaryType": "CAMPAIGN",
    "campaign": "502520fd0cf236b8a1545f8b",
    "beginOn": "2015-01-01",
    "endOn": "2015-01-21",
    "bucketSize": "DAY"
}
```
#### [MessageDetailsReportQuery](/APIModel/MessageDetailsReportQuery)
**Model**
APIModel for MessageDetailsReportQuery
```
{
    "type": "messageDetails",
    "campaign": "502520fd0cf236b8a1545f8b",
    "messageType": "MO",
    "contentType": "SUBSCRIPTION",
    "beginOn": "2015-01-01",
    "endOn": "2015-01-21"
}
```
#### [PollResultsReportQuery](/APIModel/PollResultsReportQuery)
**Model**
APIModel for PollResultsReportQuery
```
{
    query: {
        "type": "pollSummary",
        "mobileFlow": "mobileFlowId"
    },
    "scheduleAt": "2014-12-24T16:00:00.727-05:00",
    "name": "Poll Summary for Mobile Flow SomeCampaignName"
}
```
#### [Shortcode](/APIModel/Shortcode)
**Model**
APIModel for Shortcode
```
{
    "id": "5493568f0cf2fcad2e35ecb5",
    "provider": "AggregateUS",
    "countryCode": "1",
    "dedicated": true,
    "description": "RevMsg",
    "maxSmsLength": 160,
    "profileId": "98765",
    "shortcode": "675309",
    "testPrefix": null,
    "defaultStopResponse": "You will not receive any more mobile updates from {subscriber.recentMf.programName; default=\"RevMsg\"}.",
    "defaultHelpResponse": "Mobile updates from {subscriber.recentMf.programName; default=\"RevMsg\"}. Reply STOP to quit. Msg&Data rates may apply. Tech support: sms@txthlp.com",
    "carrierStopResponses": {},
    "carrierHelpResponses": {},
    "status": "ACTIVE",
    "forwardURL": null,
    "internalProcessing": null,
    "sessionTimeout": 10800000,
    "mms": false
}
```

#### [SmartListRequest](/APIModel/SmartListRequest)
**Model**
APIModel for SmartListRequest
```
{
    "lists": ["548f5cd20cf2f50c89c05ab8"],
    "queryFilterDetails": {
        "operator": "OR",
        "details": [{
            "metadata": "546239d10cf25fdcf0aea9bc",
            "operator": "=",
            "value": "510"
        },
        {
            "metadata": "548f5f3b0cf2f50c89c15385",
            "operator": "=",
            "value": "7"
        }
    ]},
    "name": "510 areacode OR chose 7"
}
```
#### [SmartListResponse](/APIModel/SmartListResponse)
**Model**
APIModel for SmartListResponse
```
{
    "id":"5493568f0cf2fcad2e35ecb5",
    "account":"546239d10cf25fdcf0aea9b2",
    "group":"54623a230cf25fdcf0aeaa5c",
    "shortCode":"515b0768ca10e4ec580fcc60",
    "queryFilterDetails":{
        "operator":"or",
        "details":[
            {
                "metadata":"546239d10cf25fdcf0aea9bc",
                "operator":"=",
                "value":"510",
                "radius":null
            },
            {
                "metadata":"548f5f3b0cf2f50c89c15385",
                "operator":"=",
                "value":"7",
                "radius":null
            }
        ]
    },
    "lists":["548f5cd20cf2f50c89c05ab8"],
    "name":"510 areacode OR chose 7"
}
```
#### [AccountRequest](/APIModel/AccountRequest)

**Model**
APIModel for AccountRequest
```
{
    "name": "Jon Doe",
    "password": "thiswouldbeareallybadactualpassword",
    "shortCode":"515b0768ca10e4ec580fcc60",
    "userName": "jondoe"
}
```
#### [AccountResponse](/APIModel/AccountResponse)

**Model**
APIModel for AccountResponse
```
{
    "account": "546239d10cf25fdcf0aea9b2",
    "group":"54623a230cf25fdcf0aeaa5c",
    "role": "4fd220440cf2c16d2fa79ac0",
    "user": "4eea05e50cf29daf65b1d3e0",
    "username": "jondoe"
}
```
#### [Authenticate](/APIModel/Authenticate)
**Model**
APIModel for Authenticate
```
{
    "password": "thiswouldbeareallybadactualpassword",
    "username": "jondoe"
}
```
#### [Campaign](/APIModel/Campaign)
**Model**
APIModel for Campaign
```   
{
    "account": "546239d10cf25fdcf0aea9b2",
    "endDate": null,
    "group":"54623a230cf25fdcf0aeaa5c",
    "id": "5493568f0cf2fcad2e35ecb5",
    "mobileFlows": [
        "4edfcb2a0cf2146271ed7e46",
        "4eea18df0cf29daf65b1e9e9",
        "4eea18e60cf29daf65b1ea01"
    ],
    "name": "sample",
    "shortCode":"515b0768ca10e4ec580fcc60",
    "startDate": "Fri Aug 10 09:55:57 CDT 2012",
    "status": "ACTIVE"
}
```
#### [CatchAll](/APIModel/CatchAll)
**Model**
APIModel for CatchAll
```   
{
    "dateReceived": "2012-11-04",
    "id": "5493568f0cf2fcad2e35ecb5",
    "list":"548f5cd20cf2f50c89c05ab8",
    "msg": "Can you hear me now?",
    "msisdn": "0012022999393",
    "shortCode":"515b0768ca10e4ec580fcc60",
    "shortCodeIdString": "",
    "status": "ACTIVE",
    "subscriber": ""
            }
```
#### [CatchAllCounter](/APIModel/CatchAllCounter)
**Model**
APIModel for CatchAllCounter
```   
{
    "total": "81800"
}
```
#### [Collection](/APIModel/Collection)
**Model**
APIModel for Collection
```  
{
    "collection": [],
    "page": "1",
    "size": "60",
    "total": "81800"
}
```
#### [SubscriberCountCollection](/APIModel/SubscriberCountCollection)
**Model**
```
{
    "page": null,
    "size": null,
    "total": 3092,
    "collection": []
}
```
#### [ContentModule](/APIModel/ContentModule)
**Model**
APIModel for ContentModule
```
{
    "head": "4eeb60220cf29daf65b3751e",
    "type": "SUBSCRIPTION",
    "params": {
        "subscribedSubject": null,
        "confirmSubject": null,
        "listId": "4ec68c8d0cf2a3b767982188",
        "optInType": "singleOptIn",
        "confirmFiles": [],
        "subscribedFiles": [],
        "subscribedMessage": "You already texted in, what more do you expect?",
        "confirmMessage": "Thanks for joining the Revolution staff test list. NOW GET BACK TO WORK!"
    }
}
```
#### [SubscriberMessagesResponse](/APIModel/SubscriberMessagesResponse)
**Model**
APIModel for SubscriberMessagesResponse
```
{
    "msisdn": "",
    "messages": []
}
```
#### [EditMobileFlow](/APIModel/EditMobileFlow)
**Model**
APIModel for EditMobileFlow
```
{
    "campaign": "5493568f0cf2fcad2e35ecb5",
    "id": "5493568f0cf2fcad2e35ecb5",
    "keywords": [
        {
            "id": "4ec68cef0cf2a3b7679821ab",
            "account": null,
            "group": null,
            "shortCode": null,
            "name": "rmstaff",
            "mobileFlow": null
        }
    ],
    "mobileFlow": "4edfcb2a0cf2146271ed7e46",
     "modules": []
}
```
#### [Geospatial](/APIModel/Geospatial)
**Model**
APIModel for Geospatial
``` 
{
    "centerZipcode": "20036",
    "radius": "50",
    "zipcodes": [
        "17329",
        "17331",
        "17332
    ]
}
```
#### [Group](/APIModel/Group)
**Model**
APIModel for Group
```
{
    "account": "546239d10cf25fdcf0aea9b2",
    "createdBy": "5493568f0cf2fcad2e35ecb5",
    "creationDate": "Fri Aug 10 09:55:57 CDT 2012",
    "id": "5493568f0cf2fcad2e35ecb5",
     "name": "sample"
}
```
#### [Keyword](/APIModel/Keyword)
**Model**
APIModel for Keyword
```   
{
    "account": "546239d10cf25fdcf0aea9b2",
    "group":"54623a230cf25fdcf0aeaa5c",
    "id": "5493568f0cf2fcad2e35ecb5",
    "mobileFlow": "4edfcb2a0cf2146271ed7e46",
    "name": "sample",
    "shortCode": "4e8b4b5afda5efeeec370e8a"
}
```
#### [KeywordAvailable](/APIModel/KeywordAvailable)
**Model**
APIModel for KeywordAvailable
```       
{
    "available": true,
    "name": "sample"
}
```
#### [List](/APIModel/List)
**Model**
APIModel for List
```  
{
    "account": "546239d10cf25fdcf0aea9b2",
    "createdBy": "5493568f0cf2fcad2e35ecb5",
    "group":"54623a230cf25fdcf0aeaa5c",
    "id": "5493568f0cf2fcad2e35ecb5",
    "name": "sample",
    "noOfSubscribers": "81800",
    "shortCode":"515b0768ca10e4ec580fcc60",
    "status": "ACTIVE"
}
```
#### [Messaging](/APIModel/Messaging)
**Model**
APIModel for Messaging
```   
{
    "campaign": "5493568f0cf2fcad2e35ecb5",
    "filteredLists": [
        "54dd29ed0cf21202213a7a8e"
    ],
    "id": "5493568f0cf2fcad2e35ecb5",
    "message": "Hey, what's up?"
    "mobileFlow": "4edfcb2a0cf2146271ed7e46",
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
    ],
    "msisdns": [
        "0012022999393"
    ],
    "programName": "Test Campaign",
    "schedule": "Thu Feb 12 17:32:26 EST 2015",
    "segments": [
        {
            "percent": 50,
            "message": "Hey, what's up?"
        },
        {
            "percent": 50,
            "message": "How YOU doin'?"
        }
    ],
    "shortCode":"515b0768ca10e4ec580fcc60"
}
```
#### [Metadata](/APIModel/Metadata)
**Model**
APIModel for Metadata
```
{
    "id": "54dd2c1e0cf21202213a7e84",
    "account": "4e6fa6177a475eefd68fb5ef",
    "group": "4e6fa6187a475eefd68fb5f5",
    "format": "[0-9]{1,2}",
    "name": "shoe size",
    "scope": "GROUP",
    "multiValue": false,
    "validValues": null,
    "eventUrl": "http://tools.revmsg.net/metadataHandler",
    "status": "ACTIVE"
}
```
#### [MetadataValue](/APIModel/MetadataValue)
**Model**
APIModel for MetadataValue
```
{
    "id": "54dd2c1e0cf21202213a7e84",
    "name": "shoe size",
    "value": "12"
}
```
#### [MobileFlow](/APIModel/MobileFlow)
**Model**
APIModel for MobileFlow
``` 
{
    "account": "546239d10cf25fdcf0aea9b2",
    "campaign": "5493568f0cf2fcad2e35ecb5",
    "group":"54623a230cf25fdcf0aeaa5c",
    "id": "5493568f0cf2fcad2e35ecb5",
    "name": "sample",
    "programName": "Sample Program",
    "shortCode":"515b0768ca10e4ec580fcc60",
    "status": "ACTIVE"
}
```

#### [QueryFilterDetailRequest](/APIModel/QueryFilterDetailRequest)
**Model**
APIModel for QueryFilterDetailRequest
```   
{
    "metadata": "54dd2c1e0cf21202213a7e84",
    "operator": "in",
    "radius": null,
     "value": "11,12,13"
}
```
#### [QueryFilter](/APIModel/QueryFilter)
**Model**
APIModel for QueryFilter
```   
{
    "account": "546239d10cf25fdcf0aea9b2",
    "group":"54623a230cf25fdcf0aeaa5c",
    "id": "5493568f0cf2fcad2e35ecb5",
    "lists": [
        "54d001740cf2c7c3bf30a6e4",
        "54cffeca0cf2c7c3bf30a289"
    ],
    "name": "sample",
    "queryFilterDetails": [
        {
            "metadata": "54dd2c1e0cf21202213a7e84",
            "operator": "in",
            "radius": null,
            "value": "11,12,13"
        }
    ],
     "shortCode": "4e8b4b5afda5efeeec370e8a"
}
```
#### [QueryFilterDetail](/APIModel/QueryFilterDetail)
```  
{
    "metadata": "54dd2c1e0cf21202213a7e84",
    "operator": "in",
    "radius": null,
    "value": "11,12,13"
}
```
#### [QueryFilterDetailResponse](/APIModel/QueryFilterDetailResponse)
**Model**
APIModel for QueryFilterDetailResponse
```
{
    "metadata": "54dd2c1e0cf21202213a7e84",
    "operator": "in",
    "radius": null,
    "value": "11,12,13"
}
```
#### [QueryFilterRequest](/APIModel/QueryFilterRequest)
**Model**
APIModel for QueryFilterRequest
```  
{
    "account": "546239d10cf25fdcf0aea9b2",
    "details": [
        {
            "metadata": "54dd2c1e0cf21202213a7e84",
            "operator": "in",
            "radius": null,
            "value": "11,12,13"
        }
    ],
    "group":"54623a230cf25fdcf0aeaa5c",
    "id": "5493568f0cf2fcad2e35ecb5",
    "lists": [
        "54d001740cf2c7c3bf30a6e4",
        "54cffeca0cf2c7c3bf30a289"
    ],
    "name": "sample",
    "shortCode": "4e8b4b5afda5efeeec370e8a"
}
```
#### [QueryFilterResponse](/APIModel/QueryFilterResponse)
**Model**
APIModel for QueryFilterResponse
```   
{
    "account": "546239d10cf25fdcf0aea9b2",
    "group":"54623a230cf25fdcf0aeaa5c",
    "id": "5493568f0cf2fcad2e35ecb5",
    "lists": [
        "54d001740cf2c7c3bf30a6e4",
        "54cffeca0cf2c7c3bf30a289"
    ],
    "name": "sample",
    "queryFilterDetails": [
        {
            "metadata": "54dd2c1e0cf21202213a7e84",
            "operator": "in",
            "radius": null,
            "value": "11,12,13"
        }
    ],
    "shortCode": "4e8b4b5afda5efeeec370e8a"
}
```
#### [ComplexFilter](/APIModel/Query/ComplexFilter)
**Model**
APIModel for complex filter queries
```
{
    "name": "complicatedfilter",
    "lists": [
        "54cffeca0cf2c7c3bf30a289",
        "54d001740cf2c7c3bf30a6e4"
    ],
        "queryFilterDetails": {
        "operator":"AND",
        "details":[
            {
                "value": "21",
                "operator": ">=",
                "metadata": "metadataId"
            },
            {
                "operator":"OR",
                "details": [
                    {
                        "value": "214",
                        "operator": "=",
                        "metadata": "metadataId"
                    },
                    {
                        "value": "972",
                        "operator": "=",
                        "metadata": "metadataId"
                    }
                ]
            }
        ]
    }
}
```
#### [ReportingStatus](/APIModel/ReportingStatus)
**Model**
APIModel for ReportingStatus
```   
{
    lag: 7
    status: "ONLINE"
}
```
#### [ReportingTemplateRequest](/APIModel/ReportingTemplateRequest)
**Model**
APIModel for ReportingTemplateRequest
```   
{
    "id": null,
    "account": null,
    "group": null,
    "shortCode": null,
    "name": null,
    "lastReport": null,
    "query": {
        "type": "messageDetails",
        "campaign": "502520fd0cf236b8a1545f8b",
        "messageType": "MO",
        "contentType": "SUBSCRIPTION",
        "beginOn": "2015-01-01",
        "endOn": "2015-01-21"
    }
}
```
#### [ReportingTemplateResponse](/APIModel/ReportingTemplateResponse)
**Model**
APIModel for ReportingTemplateResponse
```
{
    "id": "reportId",
    "account": "accountId",
    "group": "groupId",
    "shortCode": "shortCodeId",
    "name": "Poll Summary for Mobile Flow SomeCampaignName",
    "lastReport": {
        "file": null,
        "status": "NEW",
        "submittedAt": "2014-09-01T08:42:39.539-05:00",
        "completedAt": null,
        "scheduledAt": "2014-12-24T15:00:00.727-06:00"
    },
    "query": {
        "type": "pollSummary",
        "mobileFlow": "mobileFlowId"
    }
} 
```
#### [Role](/APIModel/Role)
**Model**
APIModel for Role
```
{
    "account": "546239d10cf25fdcf0aea9b2",
    "createdBy": "5493568f0cf2fcad2e35ecb5",
    "creationDate": "Fri Aug 10 09:55:57 CDT 2012",
    "group":"54623a230cf25fdcf0aeaa5c",
    "groupsVisible": [
        "4e6fa6187a475eefd68fb5f5"
    ],
    "id": "5493568f0cf2fcad2e35ecb5",
    "name": "sample",
    "permissions":[
        "4e6fa6177a475eefd68fb5ef:4e6fa6187a475eefd68fb5f5:*:create,read,update,delete:*",
        "4e6fa6177a475eefd68fb5ef:4e6fa6187a475eefd68fb5f4:metadata:read:*"
    ],
     "status": "ACTIVE"
}
```
#### [Security](/APIModel/Security)
**Model**
APIModel for Security
``` 
{
    "id": "5493568f0cf2fcad2e35ecb5"
}
```
#### [Segment](/APIModel/Segment)
**Model**
APIModel for Segment
``` 
{
    "percent": 50,
    "message": "Hey, what's up?",
    "value": "A"
}
```
#### [Session](/APIModel/Session)
**Model**
APIModel for Session
```
{
    "account": "546239d10cf25fdcf0aea9b2",
    "group":"54623a230cf25fdcf0aeaa5c",
    "impersonated": false,
    "isAdmin": false,
    "isGroupAdmin": false,
    "isRoot": false,
    "permissions":[
        "4e6fa6177a475eefd68fb5ef:4e6fa6187a475eefd68fb5f5:*:create,read,update,delete:*",
        "4e6fa6177a475eefd68fb5ef:4e6fa6187a475eefd68fb5f4:metadata:read:*"
    ],
    "role": "4fd220440cf2c16d2fa79ac0",
    "username": "jondoe"
}
```
#### [SessionResponse](/APIModel/SessionResponse)
**Model**
APIModel for SessionResponse
```   
{
    "account": "546239d10cf25fdcf0aea9b2",
    "group":"54623a230cf25fdcf0aeaa5c",
    "impersonated": false,
    "isAdmin": false,
    "isGroupAdmin": false,
    "isRoot": false,
    "permissions":[
        "4e6fa6177a475eefd68fb5ef:4e6fa6187a475eefd68fb5f5:*:create,read,update,delete:*",
        "4e6fa6177a475eefd68fb5ef:4e6fa6187a475eefd68fb5f4:metadata:read:*"
    ],
    "role": "4fd220440cf2c16d2fa79ac0",
    "sessionId": "5493568f0cf2fcad2e35ecb5",
    "user": "5493568f0cf2fcad2e35ecb5",
    "username": "jondoe"
}
```
#### [Subscriber](/APIModel/Subscriber)
**Model**
APIModel for Subscriber
``` 
{
    "id": "543438bf0cf25a19cdb8354e",
    "firstName": "Jon",
    "lastName": "Snow",
    "email": "jsnow@blackwatch.org",
    "facebook": "stark.bastard23",
    "twitter": "stark.bastard23",
    "mobileNumber": "0016081112222",
    "state": "WI",
    "timeZone": "-0700",
    "areaCode": "608",
    "zipCode": "54806",
    "birthDate": "1999-12-31T00:00:00.000",
    "dateAdded": "2014-12-16T13:57:02.355",
    "metadata": {
        "548f5f3b0cf2f50c89c15385": [
            "7"
        ],
        "548f64ad0cf2f50c89c39f53": [
            "12311980"
        ],
        "546239d10cf25fdcf0aea9bf": [
            "2014-12-16T13:57:02.355"
        ],
        "546239d10cf25fdcf0aea9be": [
            "1999-12-31T00:00:00.000"
        ],
        "546239d10cf25fdcf0aea9bd": [
            "54806"
        ],
        "546239d10cf25fdcf0aea9bc": [
            "608"
        ],
        "546239d10cf25fdcf0aea9bb": [
            "-0700"
         ],
        "546239d10cf25fdcf0aea9ba": [
            "WI"
        ],
        "546239d10cf25fdcf0aea9b5": [
            "Snow"
        ],
        "546239d10cf25fdcf0aea9b6": [
            "jsnow@blackwatch.org"
        ],
        "548f656a0cf2f50c89c3fc75": [
            "54806"
        ],
        "546239d10cf25fdcf0aea9b4": [
            "Jon"
        ],
        "546239d10cf25fdcf0aea9b9": [
            "0016081112222"
        ],
         "546239d10cf25fdcf0aea9b7": [
             "stark.bastard23"
        ],
        "546239d10cf25fdcf0aea9b8": [
            "stark.bastard23"
        ]
    },
    "listDetails": {
        "5094304e0cf280bc6a98bf8e": {
            "details": {
                "mobileFlow": "509430b10cf280bc6a98bff8",
                "trigger": "509430b10cf280bc6a98bff9"
            },
            "joinDate": "Thu Oct 09 11:36:14 CDT 2014",
            "source": "MOBILE"
        },
        "4f3454170cf25b1ca44caf6a": {
            "details": {
                "mobileFlow": "54934e240cf2a36986b4770f",
                "trigger": "54934e240cf2a36986b47710"
            },
            "joinDate": "Thu Dec 18 15:59:27 CST 2014",
            "source": "MOBILE"
        }
    },
    "blacklist": []
}
```
#### [SubscribersAndList](/APIModel/SubscribersAndList)
**Model**
APIModel for SubscribersAndList
```  
{
    "list":"548f5cd20cf2f50c89c05ab8",
    "subscribers": ""
}
```
#### [Trigger](/APIModel/Trigger)
**Model**
APIModel for Trigger
```   
{
    "account": "546239d10cf25fdcf0aea9b2",
    "creationDate": "Fri Aug 10 09:55:57 CDT 2012",
    "group":"54623a230cf25fdcf0aeaa5c",
    "mobileFlow": "4edfcb2a0cf2146271ed7e46",
    "name": "sample",
    "shortCode": "4e8b4b5afda5efeeec370e8a"
}
```
#### [User](/APIModel/User)
**Model**
APIModel for User
```
{
    "account": "546239d10cf25fdcf0aea9b2",
    "apiKey": "2baa7764-f2fa-4b07-b5de-867dd8ee2532",
    "createdBy": "5493568f0cf2fcad2e35ecb5",
    "defaultshortCode": "4e8b4b5afda5efeeec370e8a",
    "details": {
        "name": "Jon Doe",
        "title": "Communications Director",
        "phone": "0012022999393",
        "mobile": "0012022999393",
        "email": "jondoe@shormakers.org",
        "company": "Shoemakers International Union",
        "lastLogin": null
    },
    "group":"54623a230cf25fdcf0aeaa5c",
    "id": "5493568f0cf2fcad2e35ecb5",
    "name": "sample",
    "password": "thiswouldbeareallybadactualpassword",
    "role": "4fd220440cf2c16d2fa79ac0",
     "shortCodes": [
        "4e8b4b5afda5efeeec370e8a"
     ],
    "status": "ACTIVE"
}
```
#### [UserDetails](/APIModel/UserDetails)
**Model**
APIModel for UserDetails
```  
{
    "name": "Jon Doe",
    "title": "Communications Director",
    "phone": "0012022999393",
    "mobile": "0012022999393",
    "email": "jondoe@shoemakers.org",
    "company": "Shoemakers International Union"
}
```
### Group Authenticate

These methods deal with logging into and out of the platform.

*Authenticate* model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| password  | string    | true  | The password  |
| username  | string    | true  | The user name.    |

*Session* model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | true  | User's account ID |
| group | string    | true  | User's group ID   |
| impersonated  | boolean   | true  | Currently impersonated    |
| isAdmin   | boolean   | true  | Admin session |
| isGroupAdmin  | boolean   | true  | Group admin session   |
| isRoot    | boolean   | true  | Root session  |
| permissions   | list  | true  | Permission strings of user's role |
| role  | string    | true  | User's role ID    |
| sessionId | string    | true  | Session ID    |
| user  | string    | true  | User ID   |
| username  | string    | true  | User's login ID   |

#### v1
**log in**
```
POST /v1/authenticate
```
**Request**
```
[Authenticate][]
```
**Response**
```
Status: 204
```
**Response**
```
Status: 401
```
* * *
Retrieve information on your currently-active session
```
GET /v1/authenticate/whoami
```
**Response**
``` 
Status: 200
[SessionResponse][]
```
**Response**
```
Status: 401
```
**Response**
```
Status: 403
```
* * * 
End your authentication session
```
POST /v1/authenticate/logout
```
**Response**
```
Status: 204
```
**Response**
```
Status: 401
```
**Response**
```
Status: 403
```
#### v2
**log in**
```
POST /v2/authenticate
```
**Request**
```
[Authenticate][]
```
**Response**
```
Status: 200
[Session][]
```
**Response**
```
Status: 401
```
**Response**
```
Status: 403
```
* * *
Retrieve information on your currently-active session
```
GET /v2/authenticate/whoami
```
** Response**
```
Status: 200
[SessionResponse][]
  ```
**Response**
```
Status: 401
```
**Response**
```
Status: 403
```
### Group Broadcast

Use the Broadcast API to retrieve and cancel scheduled broadcasts.

#### v2
##### Parameters
id (optional, 24 char hex) ... the THING's unique identifier. Required in PUT & DELETE requests, and in GET requests to retrieve information about a specific broadcast.

##### get broadcast
```
GET /v2/broadcast/{id}
```
Retrieve information about a specific broadcast if {id} is specified, or a collection of scheduled broadcasts with pagination parameters if {id} is absent
##### Response
```
Status: 200
[BroadcastResponse][]
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
##### delete broadcast
```
DELETE /v2/broadcast/{id}
```
Cancel a specific scheduled broadcast
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
##### create broadcast
```
POST /v2/broadcast/{id}
```
Send or schedule a broadcast
##### Request
```
[BroadcastRequest][]
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

### Campaign
All outbound messages and any object that can send an outbound message on the platform must be associated with a campaign. Use campaigns to organize your mobile program.

*Campaign* model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | false | The ID of the account that contains this campaign.    |
| endDate   | Date  | false | The ending date of the campaign.  |
| group | string    | false | The ID of the group that contains this campaign.  |
| id    | string    | false | The ID of this campaign.  |
| mobileFlows   | list  | false | A list of the mobile flows assigned to this campaign. |
| name  | string    | false | The name of the campaign. |
| shortCode | string    | false | The ID of the short code for this campaign.   |
| startDate | Date  | false | The starting date of the campaign.    |
| status    | string    | false | Flag indicating whether this campaign is currently active.    |

#### v1
##### Parameters
id (optional, 24 char hex) ... the campaign's unique identifier. Required in GET, PUT & DELETE requests.
##### get campaign
```
GET /v1/campaign/{id}
```
##### Response
```
Staus: 200
[Campaign][]
```
##### delete campaign
```
DELETE /v1/campaign/{id}
```
##### Response
```
Status: 204
```
##### update campaign
```
Status: PUT
```
##### Request
```
[Campaign][]
```
##### Response
```
Status: 204
```
* * * 
Create a new campaign
```
POST /v1/campaign/
```
##### Request
```
[Campaign][]
```
##### Response
```
Status: 200
[Campaign][]
```
* * *
Retrieve a collection of campaigns
```
GET /v1/campaign
```
##### Response
```
Status: 200
[Collection][]
```
### Catchall/Inbox

*Catch-all counter* model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| total | string    | false | The number of inbox messages for a specific account, group, and short code.   |

*Catch-all* model

|property  | type  | required  | description   |
|-----|-----|-----|-----|
| dateReceived  | Date  | false | The date the message was received.    |
| id    | string    | false | The ID of the inbox message.  |
| list  | string    | false | The ID of the lists to which this subscriber is joined. |
| msg   | string    | false | The body of the message.  |
| msisdn    | string    | false | The 13-digit mobile phone number the subscriber.  |
| shortCode | string    | false | The ID of the short code that contains this message.  |
| shortCodeIdString | string    | false | The short code number that contains this message. |
| status    | string    | false | Indicates whether this inbox message is currently active. Deleted inbox messages are marked INACTIVE and will not be retrieved in the future.  The allowable values are 'ACTIVE' and 'INACTIVE'. This element is case-sensitive.  |
| subscriber    | string    | false | The ID of the subscriber that wrote this message. |

#### v1
##### Parameters
id (optional, 24 char hex) ... a message's unique identifier. Required in GET, PUT & DELETE requests.
##### delete an inbox message
```
DELETE /v1/catchAll/{id}
```
##### Response
```
Status: 204
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
Status: 404
```
##### Response
```
Status: 500
```
* * *
Retrieve the number of messages in the inbox
```
GET /v1/catchAll/inboxCounter
```
##### Response
```
Status: 200
[CatchAllCounter][]
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
Retrieve inbox messages
```
GET /api/v1/catchAll
```
##### Response
```
Staus: 200
[CatchAll][]
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

### Filter
Filters consist of a set of lists, a set of metadata-based criteria, and are used to retrieve dedpulicated collections of subscribers who are on one or more of the component lists and fit the criteria. v1 of the filter API allows only the simpler filters described with the `QueryFilter` model, below. These filters are limited to a set of AND criteria, including only subscribers who match all of the criteria in the filter. v2 of the API is backward-compatible, accepting the same models as v1, but also allows for the `ComplexFilter` model, which incorporates both AND and OR matches and also allows for arbitrary levels of recursion, as `ComplexFilterDetail` objects may be nested in the `details` property of other `ComplexFilterDetail` objects.

The `QueryFilter` model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | false | The ID of the account that contains this query filter.    |
| group | string    | false | The ID of the group that contains this filter.    |
| id    | string    | false | The ID of this query filter.  |
| lists | list  | true  | An array of list IDs. This element must contain at least one list ID. |
| name  | string    | false | The name of the query filter. |
| queryFilterDetails    | array |true   | collection of at least one `QueryFilterDetails` object |
| shortCode | string    | false | The ID of the short code that contains this filter.   |

`ComplexFilter` model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| name  | string    | false | human-readable name for the filter |
| lists | array |   true    | array of lists included as a source for the filter    |
| queryFilterDetails    | object   | true  | a `ComplexFilterDetails` object describing the filter criteria |

`QueryFilterDetail` model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| metadata  | string    | true  | Metadata Id   |
| operator  | string    | true  | Operator  |
| value | string    | true  | Metadata value    |

`ComplexFilterDetails` model 

| property  | type  | required  | description   |
|-----|-----|-----|-----| 
| operator  | "OR" or "AND" |   true    | type of match
| details   | array | true  | collection of at least one `ComplexFilterDetails` and `QueryFilterDetails` object |

`Geospatial` model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| centerZipcode | string    | true  | The ZIP code that is the center of the described area.    |
| radius    | string    | true  | The radius in miles around a representative location for the center ZIP code. |
| zipcodes  | list  | false | The ZIP codes that fall partially or completely within the described area, including the center ZIP code. |


#### v1
##### Parameters
id (optional, 24 char hex) ... the filter's unique identifier. Required in GET, PUT & DELETE requests.
##### get query filter
```
GET /v1/filter/{id}
```
Retrieve a filter by ID. This endpoint is capable of retrieving complex as well as simple filters, though complex filters may only be created or updated using the v2 endpoint.
##### Response
```
Status: 200
[QueryFilter][]
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
##### update query filter
```
PUT /v1/filter/{id}
```
##### Request
```
[QueryFilter][]
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

##### delete query filter
```
DELETE /v1/filter/{id}
```
Delete a filter by ID. This endpoint is capable of deleting complex as well as simple filters, though complex filters may only be created or updated using the v2 endpoint.
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
##### create query filter
```
POST /v1/filter/{id}
```
##### Request
```
[QueryFilter][]
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
Use this method to retrieve all ZIP codes within a radius of another ZIP code. The response from this endpoint is usually used to build a filter for subscribers near a certain location.
```
GET /v1/filter/zipcode 
```
##### Response
```
Status: 200
[Geospatial][]
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
Example payloads here use the `ComplexFilter` model, though this endpoint accepts `QueryFilter` objects as well.
##### Parameters
  + id (optional, 24 char hex) ... the filter's unique identifier. Required in GET, PUT & DELETE requests.
##### Update an existing query filter
```
PUT /v2/filter/{id}
```
##### Request
```
[ComplexFilter][]
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
##### Create a new query filter 
```
POST /v2/filter/{id}
```
##### Request
```
[ComplexFilter][]
```
##### Response 
```
Status: 200
[ComplexFilter][]
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
### Group Group
All platform objects are associated with a group, and role permissions are exercised over the group.

*Group* Model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | false | Account   |
| createdBy | string    | false | Created by user   |
| creationDate  | Date  | false | Creation date |
| id    | string    | false | Object ID |
| name  | string    | false | Name  |


#### v1
##### Parameters
id (optional, 24 char hex) ... the campaign's unique identifier. Required in GET, PUT & DELETE requests.
##### get
```
GET /v1/group/{id}
```
Retrieve group specified by ID
##### Response 
```
Status: 200
[Group][]
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

##### delete
```
DELETE /v1/group/{id}
```
Delete group specified by ID

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

##### update
```
PUT /v1/group/{id}
```
Update a group by ID

##### Request
```
[Group][]
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

##### create
```
POST /v1/group/{id}
```
Create a new group
##### Request
```
[Group][]
```
##### Response 
```
Status: 200
[Group][]
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
Retrieve groups by filter and pagination parameters
```
GET /v1/group
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

### Group Impersonate
Impersonate allows master admin users to alter their session to act as if they were another user.

#### v1
##### Parameters
user (optional, 24 char hex) ... the unique identifier of the user to be impersonated.
##### release
```
DELETE /v1/impersonate/{user}
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
##### Response 403
```
Status: 403
```
##### Response 500
```
Status: 500
```

##### impersonate
```
POST /v1/impersonate/{user}
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
##### Response 403
```
Status: 403
```
##### Response 500
```
Status: 500
```

### List
Lists are collections of mobile subscribers. Lists may be used in broadcasts or in the creation of filters.

#### v1

##### Parameters
id (optional, 24 char hex) ... the campaign's unique identifier. Required in GET, PUT & DELETE requests.

##### get list
```
GET /v1/list/{id}
```
##### Response 
```
Status: 200
[List][]
```
##### Response 
```
Status: 400
```
##### Response
```
Status: 401
```
##### Response 403
```
Status: 403
```
##### Response 500
```
Status: 500
```
 
##### delete list
```
DELETE /v1/list/{id}
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
##### Response 403
```
Status: 403
```
##### Response 500
```
Status: 500
```

##### update list
```
PUT /v1/list/{id}
```
##### Request
```
[List][]
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
##### Response 403
```
Status: 403
```
##### Response 500
```
Status: 500
```

##### create list
```
POST
```
##### Request
```
[List][]
```
##### Response 
```
Status: 200
[List][]
```
##### Response 
```
Status: 400
```
##### Response
```
Status: 401
```
##### Response 403
```
Status: 403
```
##### Response 500
```
Status: 500
```

### Group Messaging
Messaging methods allow you to send broadcasts and one-off messages from the platform.

`Messaging` model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| campaign  | string    | false | The ID of the campaign with which to associate this content.  |
| filteredLists | list  | false | The IDs of the filters that describe the subscribers to which to send content.    |
| frequency | string    | false | In relation to this content, the maximum number of messages per month that will be sent to each subscriber.   |
| id    | string    | false | The ID of this content.   |
| message   | string    | false | The text of the message to send.  |
| metadata  | string    | false | Metadata for segment tagging. |
| mobileFlow    | string    | false | The ID of the mobile flow that describes the content to send. |
| modules   | Array | false | A list of content modules that describe the content to send.  |
| msisdns   | list  | false | The mobile numbers of the subscribers to which to send the content.   |
| programName   | string    | false | The name of the program with which to associate this content. |
| schedule  | date  | false | The date and time after which to send the message. The default is to send the message or broadcast immediately.   |
| segments  | Array | false | Segments for an A/B split broadcast.  |
| shortCode | string    | false | The ID of the short code that contains this message.  |
| subscribers   | list  | false | The IDs of the subscribers to which to send the content.  |
| tags  | array | false | The tags with which to label any messages associated with this content.   |

### Group Metadata
Metadata methods deal with the metdata fields the platform uses to store subscriber data. See the Subscriber methods for manipulating the metadata on individual subscribers.

`Metadata` model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | false | The ID of the account that contains this metadata field.  |
| eventUrl  | string    | false | The URL to call when this metadata field is updated for a subscriber. The URL can contain substitution strings.   |
| format    | string    | false | A regular expression that describes the valid format for this metadata field. |
| group | string    | false | The ID of the group that contains this metadata field.    |
| id    | string    | false | The ID of this metadata field.    |
| multiValue    | boolean   | false | Indicates whether this metadata field can contain multiple values for a given subscriber. |
| name  | string    | false | The name of the metadata field.   |
| scope | string    | false | The scope in which the metadata field is defined. Valid values are 'SYSTEM', 'PROFILE', ACCOUNT', and 'GROUP'. 'SYSTEM' indicates that the field is defined for all accounts. 'PROFILE' indicates that this field is defined for all groups within the account that contains this metadata field, but is read only. 'ACCOUNT' indicates that the field is defined for all groups within the account that contains this metadata field. 'GROUP' indicates that the field is only available within the group and account that contain the field.    |
| status    | string    | false | Indicates whether this metadata field is currently active.    |
| validValues   | list  | false | An array of valid values for this metadata field. |

#### v1

##### Parameters
id (optional, 24 char hex) ... the metadata field's unique identifier. Required in GET, PUT & DELETE requests.

##### get metadata
```
GET /v1/metadata/{id}
```
##### Response 
```
Status: 200
[Metadata][]
```
##### Response 
```
Status: 400
```
##### Response
```
Status: 401
```
##### Response 403
```
Status: 403
```
##### Response 500
```
Status: 500
```
 
##### delete metadata
```
DELETE /v1/metadata/{id}
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
##### Response 403
```
Status: 403
```
##### Response 500
```
Status: 500
```

##### update metadata

##### PUT /v1/metadata/{id}
##### Request
```
[Metadata][]
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

##### create metadata
```
POST /v1/metadata/{id}
```
##### Request
```
[Metadata][]
```
##### Response 
```
Status: 200
[Metadata][]
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
#### Share Metadata

This method grants a role other than your own access to a metadata field. Users with that role will have all the permissions they have with metadata generally on this field.

##### Parameters
+ metadataId (required, 24 char hex) ... the unique identifier of the metadata field to be shared. 
+ roleId (required, 24 char hex) ... the unique identifier of a role which the metadata field is to be shared with.
```
POST /v1/metadata/{metadataId}/share/{roleId}
```
##### Request
```
Accept: application/json
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

### Group Mobileflow

`MobileFlow` model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | false | The ID of the account that contains this mobile flow. |
| campaign  | string    | false | The ID of the campaign to which this mobile flow is assigned; or null, if the mobile flow is not assigned to a campaign.  |
| frequency | string    | false | The maximum number of messages per month that the mobile flow will send to any one subscriber.    |
| group | string    | false | The ID of the group that contains this mobile flow.   |
| headNodes | list  | false | The IDs of the content modules in this mobile flow.   |
| id    | string    | false | The ID of this mobile flow.   |
| name  | string    | false | The name of the mobile flow.  |
| programName   | string    | false | The name of the program with which to associate this mobile flow. |
| shortCode | string    | false | The ID of the short code for this mobile flow.    |
| status    | string    | false | Indicates whether this mobile flow is currently active.   |

`EditMobileFlow` model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| campaign  | CampaignAPIModel  | false | A sparse set of information for the campaign for which this mobile flow is associated.    |
| id    | string    | false | The ID of this mobile flow.   |
| keywords  | list  | false | An array of sparse keyword information indicating the keyword names to associate with the mobile flow.    |
| mobileflow    | MobileFlowAPIModel    | false | A sparse set of information for the mobile flow.  |
| modules   | list  | false | An array of `ContentModule` objects that define the interaction of the mobile flow.   |

`ContentModule` model

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| head  | string    | false | The ID of the head content node. This is used to uniquely identify a content module.  |
| params    | string    | false | Map of content parameters. These vary based on the type. Refer to the Content Modules section at the end of this document for a description of the parameters for each of the content types available.  |
| type  | string    | false | The content type of the content module. For a description of available content types, refer to the Content Modules section at the end of this document. |

