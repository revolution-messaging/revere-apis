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

#### [BroadcastResponse](/APIModel/BroadcastResponse(
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

+ Headers
```    
Accept: application/json
Content-Type: application/json
``` 
+ Body
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
#### Collection [/APIModel/Collection]
+ Model (application/json)
APIModel for Collection
    + Headers
    + Body
    
            {
                "collection": [],
                "page": "1",
                "size": "60",
                "total": "81800"
            }

#### SubscriberCountCollection [/APIModel/SubscriberCountCollection]
+ Model (application/json)
    + Headers
    + Body

            {
              "page": null,
              "size": null,
              "total": 3092,
              "collection": []
            }

#### ContentModule [/APIModel/ContentModule]
+ Model (application/json)
APIModel for ContentModule
    + Headers
    + Body
    
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

#### SubscriberMessagesResponse [/APIModel/SubscriberMessagesResponse]
+ Model (application/json)
  APIModel for SubscriberMessagesResponse
  + Headers
  + Body

            {
            "msisdn": "",
            "messages": []
            }

#### EditMobileFlow [/APIModel/EditMobileFlow]
+ Model (application/json)
APIModel for EditMobileFlow
    + Headers
    + Body
    
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

#### Geospatial [/APIModel/Geospatial]
+ Model (application/json)
APIModel for Geospatial
    + Headers
    + Body
    
            {
                "centerZipcode": "20036",
                "radius": "50",
                "zipcodes": [
                    "17329",
                    "17331",
                    "17332
                ]
            }

#### Group [/APIModel/Group]
+ Model (application/json)
APIModel for Group
    + Headers
    + Body
    
            {
                "account": "546239d10cf25fdcf0aea9b2",
                "createdBy": "5493568f0cf2fcad2e35ecb5",
                "creationDate": "Fri Aug 10 09:55:57 CDT 2012",
                "id": "5493568f0cf2fcad2e35ecb5",
                "name": "sample"
            }

#### Keyword [/APIModel/Keyword]
+ Model (application/json)
APIModel for Keyword
    + Headers
    + Body
    
            {
                "account": "546239d10cf25fdcf0aea9b2",
                "group":"54623a230cf25fdcf0aeaa5c",
                "id": "5493568f0cf2fcad2e35ecb5",
                "mobileFlow": "4edfcb2a0cf2146271ed7e46",
                "name": "sample",
                "shortCode": "4e8b4b5afda5efeeec370e8a"
            }

#### KeywordAvailable [/APIModel/KeywordAvailable]
+ Model (application/json)
APIModel for KeywordAvailable
    + Headers
    + Body
        
            {
                "available": true,
                "name": "sample"
              }

#### List [/APIModel/List]
+ Model (application/json)
APIModel for List
    + Headers
    + Body
    
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

#### Messaging [/APIModel/Messaging]
+ Model (application/json)
APIModel for Messaging
    + Headers
    + Body
    
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

#### Metadata [/APIModel/Metadata]
+ Model (application/json)
APIModel for Metadata
    + Headers
    + Body
    
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

#### MetadataValue [/APIModel/MetadataValue]
+ Model (application/json)
APIModel for MetadataValue
    + Headers
    + Body
    
            {
                "id": "54dd2c1e0cf21202213a7e84",
                "name": "shoe size",
                "value": "12"
            }

#### MobileFlow [/APIModel/MobileFlow]
+ Model (application/json)
APIModel for MobileFlow
    + Headers
    + Body
    
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


#### QueryFilterDetailRequest [/APIModel/QueryFilterDetailRequest]
+ Model (application/json)
APIModel for QueryFilterDetailRequest
    + Headers
    + Body
    
            {
                "metadata": "54dd2c1e0cf21202213a7e84",
                "operator": "in",
                "radius": null,
                "value": "11,12,13"
            }

#### QueryFilter [/APIModel/QueryFilter]
+ Model (application/json)
APIModel for QueryFilter
    + Headers
    + Body
    
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

#### QueryFilterDetail [/APIModel/QueryFilterDetail]
    + Headers
    + Body
    
            {
                "metadata": "54dd2c1e0cf21202213a7e84",
                "operator": "in",
                "radius": null,
                "value": "11,12,13"
            }

#### QueryFilterDetailResponse [/APIModel/QueryFilterDetailResponse]
+ Model (application/json)
APIModel for QueryFilterDetailResponse
    + Headers
    + Body
    
            {
                "metadata": "54dd2c1e0cf21202213a7e84",
                "operator": "in",
                "radius": null,
                "value": "11,12,13"
            }

#### QueryFilterRequest [/APIModel/QueryFilterRequest]
+ Model (application/json)
APIModel for QueryFilterRequest
    + Headers
    + Body
    
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

#### QueryFilterResponse [/APIModel/QueryFilterResponse]
+ Model (application/json)
APIModel for QueryFilterResponse
    + Headers
    + Body
    
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

#### ComplexFilter [/APIModel/Query/ComplexFilter]
+ Model (application/json)
APIModel for complex filter queries
    + Headers
    + Body

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

#### ReportingStatus [/APIModel/ReportingStatus]
+ Model (application/json)
APIModel for ReportingStatus
    + Headers
    + Body
    
            {
                lag: 7
                status: "ONLINE"
            }

#### ReportingTemplateRequest [/APIModel/ReportingTemplateRequest]
+ Model (application/json)
APIModel for ReportingTemplateRequest
    + Headers
    + Body
    
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


#### ReportingTemplateResponse [/APIModel/ReportingTemplateResponse]
+ Model (application/json)
APIModel for ReportingTemplateResponse
    + Headers
    + Body
    
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


#### Role [/APIModel/Role]
+ Model (application/json)
APIModel for Role
    + Headers
    + Body
    
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

#### Security [/APIModel/Security]
+ Model (application/json)
APIModel for Security
    + Headers
    + Body
    
            {
                "id": "5493568f0cf2fcad2e35ecb5"
            }

#### Segment [/APIModel/Segment]
+ Model (application/json)
APIModel for Segment
    + Headers
    + Body
    
            {
                "percent": 50,
                "message": "Hey, what's up?",
                "value": "A"
            }

#### Session [/APIModel/Session]
+ Model (application/json)
APIModel for Session
    + Headers
    + Body
    
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

#### SessionResponse [/APIModel/SessionResponse]
+ Model (application/json)
APIModel for SessionResponse
    + Headers
    + Body
    
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

#### Subscriber [/APIModel/Subscriber]
+ Model (application/json)
APIModel for Subscriber
    + Headers
    + Body
    
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

#### SubscribersAndList [/APIModel/SubscribersAndList]
+ Model (application/json)
APIModel for SubscribersAndList
    + Headers
    + Body
    
            {
                "list":"548f5cd20cf2f50c89c05ab8",
                "subscribers": ""
            }

#### Trigger [/APIModel/Trigger]
+ Model (application/json)
APIModel for Trigger
    + Headers
    + Body
    
            {
                "account": "546239d10cf25fdcf0aea9b2",
                "creationDate": "Fri Aug 10 09:55:57 CDT 2012",
                "group":"54623a230cf25fdcf0aeaa5c",
                "mobileFlow": "4edfcb2a0cf2146271ed7e46",
                "name": "sample",
                "shortCode": "4e8b4b5afda5efeeec370e8a"
            }

#### User [/APIModel/User]
+ Model (application/json)
APIModel for User
    + Headers
    + Body
    
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

#### UserDetails [/APIModel/UserDetails]
+ Model (application/json)
APIModel for UserDetails
    + Headers
    + Body
    
            {
                "name": "Jon Doe",
                "title": "Communications Director",
                "phone": "0012022999393",
                "mobile": "0012022999393",
                "email": "jondoe@shormakers.org",
                "company": "Shoemakers International Union"
            }

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

#### v1 [/v1/authenticate]

** log in [POST] **
+ Request
  [Authenticate][]

+ Response 204
+ Response 401

```
GET /v1/authenticate/whoami
```
Retrieve information on your currently-active session

+ Response 200
  [SessionResponse][]
+ Response 401
+ Response 403
```
POST /v1/authenticate/logout
```
End your authentication session

+ Response 204
+ Response 401
+ Response 403

#### v2 [/v2/authenticate]

** log in [POST] **
+ Request
  [Authenticate][]

+ Response 200
  [Session][]
+ Response 401
+ Response 403

```
GET /v2/authenticate/whoami
```
Retrieve information on your currently-active session

+ Response 200
  [SessionResponse][]
+ Response 401
+ Response 403

### Group Broadcast

Use the Broadcast API to retrieve and cancel scheduled broadcasts.

#### v2 [/v2/broadcast/{id}]

+ Parameters
    + id (optional, 24 char hex) ... the THING's unique identifier. Required in PUT & DELETE requests, and in GET requests to retrieve information about a specific broadcast.

** get broadcast [GET] **

Retrieve information about a specific broadcast if {id} is specified, or a collection of scheduled broadcasts with pagination parameters if {id} is absent

+ Response 200
    [BroadcastResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500
 
** delete broadcast [DELETE] **

Cancel a specific scheduled broadcast

+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500 

** create broadcast [POST] **

Send or schedule a broadcast
+ Request
    [BroadcastRequest][]
            
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group Campaign
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

#### v1 [/v1/campaign/{id}]

+ Parameters
  + id (optional, 24 char hex) ... the campaign's unique identifier. Required in GET, PUT & DELETE requests.

** get campaign [GET] **
+ Response 200
  [Campaign][]

** delete campaign [DELETE] **
+ Response 204

** update campaign [PUT] **
+ Request
  [Campaign][]
+ Response 204

```
POST /v1/campaign/
```
Create a new campaign
+ Request
[Campaign][]
+ Response 200
[Campaign][]

```
GET /v1/campaign
```
Retrieve a collection of campaigns
+ Response 200
  [Collection][]

### Group Catchall/Inbox

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

#### v1 [/v1/catchAll/{id}]

+ Parameters
  + id (optional, 24 char hex) ... a message's unique identifier. Required in GET, PUT & DELETE requests.

** delete an inbox message [DELETE] **
+ Response 204
+ Response 401
+ Response 403
+ Response 404
+ Response 500

```
GET /v1/catchAll/inboxCounter
```
Retrieve the number of messages in the inbox
+ Response 200
    [CatchAllCounter][]
+ Response 401
+ Response 403
+ Response 500

```
GET /api/v1/catchAll
```
Retrieve inbox messages
+ Response 200
    [CatchAll][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group Filter
Filters consist of a set of lists, a set of metadata-based criteria, and are used to retrieve dedpulicated collections of subscribers who are on one or more of the component lists and fit the criteria. v1 of the filter API allows only the simpler filters described with the `QueryFilter` model, below. These filters are limited to a set of AND criteria, including only subscribers who match all of the criteria in the filter. v2 of the API is backward-compatible, accepting the same models as v1, but also allows for the `ComplexFilter` model, which incorporates both AND and OR matches and also allows for arbitrary levels of recursion, as `ComplexFilterDetail` objects may be nested in the `details` property of other `ComplexFilterDetail` objects.

The 

`QueryFilter` model

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


#### v1 [/v1/filter/{id}]

+ Parameters
  + id (optional, 24 char hex) ... the filter's unique identifier. Required in GET, PUT & DELETE requests.

** get query filter [GET] **

Retrieve a filter by ID. This endpoint is capable of retrieving complex as well as simple filters, though complex filters may only be created or updated using the v2 endpoint.

+ Response 200
    [QueryFilter][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** update query filter [PUT] **
+ Request
    [QueryFilter][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** delete query filter [DELETE] **

Delete a filter by ID. This endpoint is capable of deleting complex as well as simple filters, though complex filters may only be created or updated using the v2 endpoint.

+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** create query filter [POST] **
+ Request
    [QueryFilter][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/filter/zipcode 
```

Use this method to retrieve all ZIP codes within a radius of another ZIP code. The response from this endpoint is usually used to build a filter for subscribers near a certain location.

+ Response 200
    [Geospatial][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

#### v2 [/v2/filter/{id}]

Example payloads here use the `ComplexFilter` model, though this endpoint accepts `QueryFilter` objects as well.

+ Parameters
  + id (optional, 24 char hex) ... the filter's unique identifier. Required in GET, PUT & DELETE requests.

** Update an existing query filter [PUT] **

+ Request
    [ComplexFilter][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500


** Create a new query filter [POST] **

+ Request
    [ComplexFilter][]
+ Response 200
    [ComplexFilter][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

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


#### v1 [/v1/group/{id}]

+ Parameters
  + id (optional, 24 char hex) ... the campaign's unique identifier. Required in GET, PUT & DELETE requests.

** get [GET] **
Retrieve group specified by ID

+ Response 200
    [Group][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** delete [DELETE] **
Delete group specified by ID

+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** update [PUT] **
Update a group by ID

+ Request
    [Group][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** create [POST] **
Create a new group
+ Request
    [Group][]
+ Response 200
    [Group][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/group
```
Retrieve groups by filter and pagination parameters

+ Response 200
    [Collection][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group Impersonate
Impersonate allows master admin users to alter their session to act as if they were another user.

#### v1 [/v1/impersonate/{user}]

+ Parameters
  + user (optional, 24 char hex) ... the unique identifier of the user to be impersonated.

** release [DELETE] **
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** impersonate [POST] **
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group List
Lists are collections of mobile subscribers. Lists may be used in broadcasts or in the creation of filters.

#### v1 [/v1/list/{id}]

+ Parameters
  + id (optional, 24 char hex) ... the campaign's unique identifier. Required in GET, PUT & DELETE requests.

** get list [GET] **
+ Response 200
    [List][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500
 
** delete list [DELETE] **
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** update list [PUT] **
+ Request
    [List][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** create list [POST] **
+ Request
    [List][]
+ Response 200
    [List][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

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

#### v1 [/v1/metadata/{id}]

+ Parameters
  + id (optional, 24 char hex) ... the metadata field's unique identifier. Required in GET, PUT & DELETE requests.

** get metadata [GET] **
+ Response 200
    [Metadata][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500
 
** delete metadata [DELETE] **
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** update metadata [PUT] **
+ Request
    [Metadata][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** create metadata [POST] **
+ Request
    [Metadata][]
+ Response 200
    [Metadata][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
POST /v1/metadata/{metadataId}/share/{roleId}
```

#### Share Metadata

This method grants a role other than your own access to a metadata field. Users with that role will have all the permissions they have with metadata generally on this field.

+ Parameters
  + metadataId (required, 24 char hex) ... the unique identifier of the metadata field to be shared. 
  + roleId (required, 24 char hex) ... the unique identifier of a role which the metadata field is to be shared with.

+ Request
    + Headers

            Accept: application/json

+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

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

#### v1 [/v1/mobileflow/{id}]

+ Parameters
  + id (required, 24 char hex) ... the mobile flow's unique identifier. Required in GET, PUT & DELETE requests.

** get mobileflow [GET] **
+ Response 200
    [MobileFlow][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500
 
** delete mobileflow [DELETE] **
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** update mobileflow [PUT] **
+ Request
    [MobileFlow][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** create mobileflow [POST] **
+ Request
    [MobileFlow][]
+ Response 200
    [MobileFlow][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

#### v2 [/v2/mobileflow/{id}]

+ Parameters
    + id (optional, 24 char hex) ... the mobile flow's unique identifier. Required in GET, PUT & DELETE requests.

** get mobileflow [GET] **
+ Response 200
    [MobileFlow][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500
 
** delete mobileflow [DELETE] **
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** update mobileflow [PUT] **
+ Request
    [MobileFlow][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** create mobileflow [POST] **
+ Request
    [MobileFlow][]
+ Response 200
    [MobileFlow][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group MO Routing

#### `moroute` model

| property  | type  | required      | description   |
|-----      |-----  |-----          |-----|
| id        | 24 char hex   | true          | the MO route's ID |
| keyword   | 24 char hex   | true          | the ID of a keyword that MOs matching the `rule` will be routed to    |
| shortCode | 24 char hex   | true          | the ID of the shortcode that the MO route works on    |
| rule      | string (regex expression) | true  | a valid regex rule; MOs to the `shortcode` that match this rule will be considered equivalent to the MO route's `keyword` |

#### v2 [/v2/moroute/{id}]

+ Parameters
  + id (optional, 24 char hex) ... the MO Route's unique identifier. Required in PUT & DELETE requests; when omitted from a GET request, returns a collection of all MO Routes.


** retrieve moroute [GET] **
+ Response 200
    [MORoute][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** create moroute [POST] **
+ Request
    [MORoute][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** update moroute [PUT] **
+ Request
    [MORoute][]
+ Response 200
    [MORoute][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** delete moroute [DELETE] **
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group Role

`Role` model

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

#### v1 [/v1/role/{id}]

+ Parameters
  + id (optional, 24 char hex) ... the role's unique identifier. Required in GET, PUT & DELETE requests.

** get role [GET] **
+ Response 200
    [Role][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500
 
** delete role [DELETE] **
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** update role [PUT] **
+ Request
    [Role][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** create role [POST] **
+ Request
    [Role][]
+ Response 200
    [Role][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

#### v2 [/v2/role/{id}]

+ Parameters
    + id (optional, 24 char hex) ... the role's unique identifier. Required in GET, PUT & DELETE requests.

** get role [GET] **
+ Response 200
    [Role][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500
 
** delete role [DELETE] **
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** update role [PUT] **
+ Request
    [Role][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** create role [POST] **
+ Request
    [Role][]
+ Response 200
    [Role][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group Reporting

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

+ Parameters
    + listId (optional, 24 char hex) ... the ID of the list whose growth is to be tracked. If both this and `filterId` are omitted, the report will be for all lists.
    + queryFilterId (optional, 24 char hex) ... the ID of the smart list whose growth is to be tracked. If both this and `listId` are omitted, the report will be for all lists.

+ Response 200
    [Collection][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/reporting/listDetails/export/{id}
```

Export list of subscribers for a specified filtered list

+ Parameters
    + id (required, 24 char hex) ... the ID of the list or smart list to be exported

+ Request
    + Headers
    
            Accept: application/csv

+ Response 200
    + Headers
    
            Content-Type: application/csv

+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/reporting/subProfile/export/{id}
```

Export subscriber messages on a specified short code. Defaults to session short code.

+ Parameters
    + id (required, 24 char hex) ... the ID of the shortcode messages will be exported from

+ Response 200
    [ReportingTemplateResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/reporting/inbox/export
```

Export inbox messages on a specified short code. Defaults to session short code.

+ Request
    [ReportingTemplateRequest][]
+ Response 200
    [ReportingTemplateResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/reporting/messageDetails
```

### messageDetailsReport

Retrieve message details report matching filter parameters

+ Request
    [ReportingTemplateRequest][]
+ Response 200
    [ReportingTemplateResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/reporting/messageDetails/export
```

### messageDetailsExport

Export message details report matching filter parameters

+ Request
    [ReportingTemplateRequest][]
+ Response 200
    [ReportingTemplateResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/reporting/messageReport
```

### messageSummaryReport

Retrieve message summary report matching filter parameters

+ Request
    [ReportingTemplateRequest][]
+ Response 200
    [ReportingTemplateResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/reporting/messageReport/{summaryObject}/export
```

### messageSummaryReportExport
Export message summary report matching filter parameters

+ Parameters
    + summaryObject (required, 24 char hex) ... ID of the object being summarized

+ Request
    [ReportingTemplateRequest][]
+ Response 200
    [ReportingTemplateResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/reporting/subscriberGrowthReport/export
```

### subscriberGrowthExport

Export subscriber growth report matching filter parameters

+ Request
    [ReportingTemplateRequest][]
+ Response 200
    [ReportingTemplateResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/reporting/messageReport/activity
```

### messageSummaryActivity

Retrieve message summary report for session short code

+ Request
    [ReportingTemplateRequest][]
+ Response 200
    [ReportingTemplateResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/reporting/broadcastSummary
```

### broadcastSummaryReport

Retrieve broadcast summary report for session short code

+ Request
    [ReportingTemplateRequest][]
+ Response 200
    [ReportingTemplateResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/reporting/broadcastSummary/export
```

### broadcastSummaryExport

Export broadcast summary report for session short code

+ Request
    [ReportingTemplateRequest][]
+ Response 200
    [ReportingTemplateResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Asynchronous Reporting [/v2/reporting/{id}]

Asynchronous reporting allows larger and more complext reports to be saved, delegated to a separate reporting server and run without impacting the resources allocated to the application as a whole.

These methods involve the creation and management of _reporting templates_, which contain a set of search parameters defining the report, the running of these templates, which applies the template's parameters to the application's current data to generate a _file_, and the retrieval of those files once the template is finished running.

Reporting data is retrieved as a downloadable CSV file.

#### Reporting Template Models

The following models are used in asynchronous reporting.

** `ReportingStatus` model **

the current state of the reporting server.

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| lag   | number    | true  | Reporting lag in minutes  |
| status    | string    | true  | Reporting service status  |

** `ReportingTemplateRequest` model **

used when submitting requests (GET, POST or PUT) having to do with reporting templates.

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | false | Account ID    |
| group | string    | false | Group ID  |
| id    | string    | false | Object ID |
| name  | string    | false | Name of the report. This name will be used for the csv generated  |
| query  | `ReportingRequestQuery` model | false | Report query details. This is specific to the type of report |
| shortCode | string    | false | Short Code ID |
 
** `ReportingTemplateResponse` model **

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

** Message Details report **

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

** Message Totals report **

an report that aggregates numbers of messages by type and interval

| property | type | required | description |
|-----|-----|-----|-----|
| type          | 'messageSummary' | true | denotes a Message Totals report |
| summaryType   |CAMPAIGN', 'MOBILEFLOW', 'KEYWORD |  |  |
| beginOn       | date  | true | the start time of the report | 
| endOn         | date  | true | the end time of the report | 
| bucketSize    |'DAY', 'WEEK', 'MONTH'     | true | the interval into which reporting data is aggregated |

** Subscriber Growth report **

a report showing the change in subscriber status for one or more lists or smart lists over time, aggregated by interval

| property | type | required | description |
|-----|-----|-----|-----|
| type          | 'subscriberGrowth' | true | denotes a Subscriber Growth report |
| lists         |   array   | true | the lists whose activity is tracked in the report |
| timeframe     | 'TODAY', 'YESTERDAY', 'THISWEEK', 'LAST7', 'LASTWEEK', 'LAST14', 'THISMONTH', 'LAST30', 'LASTMONTH', 'ALLTIME' | false | sets the time period covered by the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| beginOn       | date  | false | the start time of the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| endOn         | date  | false | the start time of the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| bucketSize    |'DAY', 'WEEK', 'MONTH'     | true | the interval into which reporting data is aggregated |

** Broadcast Summary report **

a report of all broadcasts sent by the application to one or more lists or filters for a given time period

| property | type | required | description |
|-----|-----|-----|-----|
| type          | 'broadcastSummary' | true | denotes a Broadcast Summary report |
| lists         |   array   | true | the lists whose activity is tracked in the report |
| timeframe     | 'TODAY', 'YESTERDAY', 'THISWEEK', 'LAST7', 'LASTWEEK', 'LAST14', 'THISMONTH', 'LAST30', 'LASTMONTH', 'ALLTIME' | false | sets the time period covered by the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| beginOn       | date  | false | the start time of the report; either `timeframe` or `beginOn` and `endOn` must be present | 
| endOn         | date  | false | the start time of the report; either `timeframe` or `beginOn` and `endOn` must be present | 

** Poll Results report **

a report of poll results gathered through the use of the `interactive poll` flow component

| property | type | required | description |
|-----|-----|-----|-----|
| type          | 'pollSummary' | true | denotes a Poll Results report |
| mobileFlow         |   24-char hex   | false | the ID of a mobile flow containing a poll whose reuslts are summarized in the report. |

+ Parameters
    + id (optional, 24-char hex) ... the ID of the reporting template

#### Retrieve last run report [GET]

Returns the most recent results from a reporting template. Note that the Accept header in this request is application/csv, unlike most requests made to Revere Mobile

+ Request 
    + Headers

            Accept: application/csv
        
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

#### Retrieve reporting template information by id [GET]

+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

#### Rerun report template [PUT]

updates the file associated with a reporting template for retrieval later

+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

#### Delete access to a reporting template [DELETE]

+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

#### Create a new reporting template [POST]

+ Request
    [ReportingTemplateRequest][]
+ Response 200
    [ReportingTemplateResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v2/reporting/
```

+ Response 200
    [Collection][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

``` 
GET /v2/reporting/status
```

#### Retrieve reporting status including lag

+ Response 200
    [ReportingStatus][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group Shortcode

** `shortcode` model **

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

** Change your session shortcode **

Many platform objects are tied to a specific shortcode as well as a permissions group. Use this method to change the shortcode you are working on in order to access and manipulate these objects. Because most users will have access to only one shortcode, this method will not be necessary to the majority.

+ Parameters
    + shortcodeId (required, 24-char hex) ... The ID of the shortcode you are switching to

+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

#### v1 [/v1/shortcode/{id}]

+ Parameters
    + id (optional, 24 char hex) ... The smart list's unique identifier. Required in GET, PUT & DELETE requests. Whem omitted from a GET request, the request will return a collection of all smart lists.

** get shortcode [GET] **
+ Response 200
    [Shortcode][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

#### v2 [/vs/shortcode/{id}]

** update shortcode [PUT] **

Update certain properties of a shortcode. May only be used to update the following:

* `defaultHelpResponse`
* `defaultStopResponse`
* `sessionTimeout`

+ Request
    [Shortcode][]
+ Response 200
    [Shortcode][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group Smart Lists

A smart list is similar to a persistent filter, comprised of constituent lists and criteria filters, but which is treated like a subscription list for all intents and purposes, including reporting.

** `smartlist` model **

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| id    | 24 char hex   | yes   |  the ID of the smart list; omitted from `create smart list` |
| account    | 24 char hex   | no   |  the ID of the smart list's Revere Mobile account; omitted from `create smart list` |
| group    | 24 char hex   | no   |  the ID of the smart list's permissions group; defaults to the user's default group |
| shortCode    | 24 char hex   | no   | the ID of the smart list's shortcode; defaults to the user's default shortcode  |
| queryFilterDetails    | QueryFilterDetails API model   | yes   |  API model reflecting query criteria for the smart list |
| lists    | array  | yes   |  array of lists to be included in the smart list |
| name    | string   | yes   |  human-friendly name for the smart list |


#### v2 [/v2/smartlist/{id}]

+ Parameters
    + id (optional, 24 char hex) ... The smart list's unique identifier. Required in GET, PUT & DELETE requests. Whem omitted from a GET request, the request will return a collection of all smart lists.

** create smart list [POST] **
+ Request
    [SmartListRequest][]
+ Response 200
    [SmartListResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** get smart list [GET] **
+ Response 200
    [SmartListResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** delete smart list [DELETE] **
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### POST /v2/smartlist/{smartlistid}/share/{roleid}

#### Share smart list: grant another permissions role access to the smart list.

+ Parameters
    + smartlistid (24 char hex) ... the ID of the smartlist to be shared.
    + roleid (24 char hex) ... the ID of the permissions role that should receive access to the smart list

+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group Subscriber

Subscribers are the individual members Revere Mobile interacts with.

### GET /v1/subscriber/{idOrMsisdn}

#### Retrieve subscriber by phone number or system ID

+ Parameters
    + idOrMsisdn (optional, 24 char hex or 12-digit msisdn) ... may be the subscriber's 24-char hex identifier or their mobile phone number.

+ Response 200
    [Subscriber][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### GET /v1/subscriber?search={search}

#### Retrieve subscriber by profile metadata

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

+ Parameters
    + search (optional, string) ... search query to match across all of a subscriber's profile metadata.

+ Response 200
    [Subscriber][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/subscriber/count
```

#### Retrieve the number of subscribers in a list or filter.

+ Parameters
    + listId (optional, 24 char hex) ... the ID of a list that you are counting subscribers on. Mutually exclusive with `filterId`.
    + filterId (optional, 24 char hex) ... the ID of a filter or smart list that you are counting subscribers on. Mutually exclusive with `listId`.

+ Response 200
    [SubscriberCountCollection][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/subscriber
```

#### Retrieve a paginated collection of subscribers belonging to a list or filter.

This method operates differently from other collection-retrieval methods. If retrieving a number of pages, the maximum `size` of each page is 60; passing a number greater than this or passing -1 will result in pages with 60 records each. To retrieve up to 5000 records per request, omit `page` and set `size` to any value up to 5000. Subsequent requests may contain the `lastId` parameter to retrieve following "pages" of subscribers.

+ Parameters
    + listId (optional, 24 char hex) ... the ID of a list for which to return subscribers. Mutually exclusive with `filterId`.
    + filterId (optional, 24 char hex) ... the ID of a filter for which to return subscribers. Mutually exclusive with `listId`.
    + page (optional, integer) ... the 1-based index of the page to return. The default value is 1. Omit this parameter if attempting to retrieve more than 60 results per request.
    + size (optional, integer) ... the number of items that a call to the operation will return. The default value is 20. The maximum value is 60 when `page` is included, or 5000 when paginating using the `lastId` parameter.
    + lastId (optional, 24-char hex) ... including this parameter when `page` is absent will return a collection of the specified `size`, beginning with the first subscriber following the subscriber whose ID is equal to this parameter.

+ Response 200
    [Collection][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### PUT /v1/subscriber/addMetadata/{idOrMsisdn}

#### Add a value for a metadata field to a subscriber.

+ Parameters
    + idOrMsisdn (optional, 24 char hex or 12-digit msisdn) ... may be the subscriber's 24-char hex identifier or their mobile phone number.
+ Request
    [MetadataValue][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

#### v2 [/v1/subscriber/{idOrMsisdn}?search={search}]

+ Parameters
    + idOrMsisdn (optional, 24 char hex or 12-digit msisdn) ... may be the subscriber's 24-char hex identifier or their mobile phone number with country code.
    + search (optional, string) ... search string to be matched in any of a subscriber's profile metadata. Not used when idOrMsisdn is specified.

```
GET /v2/subscriber/{idOrMsisdn}
```

Retrieve subscriber profile by ID or Mobile Number
+ Parameters
    + idOrMsisdn (required, 24 char hex or 12-digit msisdn) ... may be the subscriber's 24-char hex identifier or their mobile phone number.

+ Response 200
    [Subscriber][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
PUT /v2/subscriber/{idOrMsisdn}/list/{listId}
```

Adds a subscriber to a subscription list. **Caution: subscribing people using this method does not ensure they have been properly opted-in or welcomed to the program.** Use this method only to add an existing, legitimate subscriber to a different list, not to introduce new people to a list.

+ Parameters
    + idOrMsisdn (required, 24 char hex or 12-digit msisdn) ... may be the subscriber's 24-char hex identifier or their mobile phone number.
    + listId (required, 24 char hex or 12-digit msisdn) ... the ID of a subscription list the subscriber will be added to.
        
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v2/subscriber?listId={listId}&filterId={filterId}
```

Retrieve a collection of subscribers matching the listId and/or filterId criteria. This method operates unlike other collection methods in that it returns a maximum of 60 results per page if the `size` parameter is either -1, 60 or greater.

+ Parameters
    + listId (optional, 24 char hex) ... ID of the list whose count you are retrieving.
    + filterId (optional, 24 char hex) ... Id of the filter or smart list whose count you are retrieving.
       
+ Response 200
    [Collection][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v2/subscriber/{msisdn}/messages
```

Retrieve messages sent to and from a subscriber, with delivery status (if known)

+ Parameters
    + msisdn (required, 12-digit msisdn) ... the subscriber's mobile phone number
        
+ Response 200
    [SubscriberMessagesResponse][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
Group Blacklist
```

The blacklist is a collection of subscribers who the current shortcode is prevented from interacting with. No response will be made to any inbound messages from these subscribers and no outbound messages will ever be delivered to them. 

#### v2 [/v2/subscriber/blacklist/{idOrMsisdn}?shortCode={shortCode}]

+ Parameters
    + idOrMsisdn (required, 24 char hex or 12-digit msisdn) ... may be a subscriber's 24-char hex identifier or their mobile phone number; omitted from the _Retrieve blacklist_ method
    + shortCode (optional, 24 char hex or 12-digit msisdn) ... the shortcode to blacklist the subscriber on; defaults to the session shortcode if omitted

** Add subscriber to blacklist [POST] **
   
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** Remove subscriber from blacklist [DELETE] **
   
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** Retrieve blacklist [GET] **
   
+ Response 200
    [Collection][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group Trigger

A trigger is a platform object that can cause a message to be sent. In plain language, both broadcasts and keywords are triggers. Both can be accessed via this API endpoint, though the use of the Trigger API for broadcasts is deprecated in favor of the Broadcast API.

** `Trigger` Model **

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| account   | string    | false | Account ID    |
| creationDate  | Date  | false | Creation date |
| group | string    | false | Group ID  |
| mobileFlow    | string    | false | Mobile flow ID    |
| name  | string    | false | Trigger name  |
| shortCode | string    | false | Short code ID |

#### v1 [/v1/trigger/{id}]

+ Parameters
  + id (optional, 24 char hex) ... the trigger's unique identifier. Required in PUT & DELETE requests, and in GET requests to retrieve information about a specific trigger.

** get trigger by id [GET] **

Retrieve information on a specific trigger. When passed without the {id} parameter, this retrieves a paginated collection of all triggers.

+ Response 200
    [Trigger][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500
 
** delete trigger [DELETE] **

Remove a keyword or scheduled broadcast. The {id} parameter is required.

+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** update trigger [PUT] **

Reassign a keyword to a different mobile flow, or unassign it entirely.

+ Request
    [Trigger][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** create trigger [POST] **

Create a new keyword.

+ Request
    [Trigger][]
+ Response 200
    [Trigger][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### GET /v1/trigger/recent

Retrieve a collection of recent broadcasts by pagination parameters.

+ Response 200
    [Collection][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/trigger/isKeywordAvailable/{name}
```

Check to see whether a given keyword is available on the current shortcode.

+ Parameters
    + name (required, string) ... the keyword to check for availability

+ Response 200
    [Collection][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
GET /v1/trigger/broadcast
```

Retrieve a list of scheduled broadcasts by pagination parameters.

+ Response 200
    [Collection][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group User

Use these endpoints to control other users' access to Revere Mobile.

** `User` Model **

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

** `UserDetails` Model **

| property  | type  | required  | description   |
|-----|-----|-----|-----|
| company   | string    | false | Company   |
| email | string    | false | Email address |
| lastLogin | Date  | false | Last login date   |
| mobile    | string    | false | Mobile number |
| name  | string    | false | Name  |
| phone | string    | false | Phone number  |
| title | string    | false | Title |

#### v1 [/v1/user/{id}]

+ Parameters
  + id (optional, 24 char hex) ... the user's unique identifier. Required in PUT & DELETE requests, and in GET requests to retrieve information about a specific trigger.

** get user [GET] **

Retrieve information on a specific user with the {id} parameter set, or retrieve a collection of all users without {id}

+ Response 200
    [User][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500
 
** delete user [DELETE] **

Remove a user from the Revere Mobile platform

+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** update user [PUT] **

Change a user's properties

+ Request
    [User][]
+ Response 204
+ Response 400
+ Response 401
+ Response 403
+ Response 500

** create user [POST] **

Create a new user

+ Request
    [User][]
+ Response 200
    [User][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

```
POST /v2/user/{id}/apikey
```

Create or reset a user's API key. The user may use this key to authenticate API requests as described in Authentication, above. A note of caution: once created, an API key may not be retrieved, only reset.

+ Parameters
    + id (optional, 24 char hex) ... the ID of the user you need to create an API key for.

+ Request
    + Headers
    
            Accept: application/json
            Content-Type: application/json
        
+ Response 200
    [APIKey][]
+ Response 400
+ Response 401
+ Response 403
+ Response 500

### Group Mobile Flow Components

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

** XML Payload **

    <dynamiccontent>
        <endSession>true</endSession>
        <response>response text</response>
    </dynamiccontent>
     

** JSON Payload **
 
    {
      "endSession": true,
      "response": "response text"
            }
      
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

### Group Examples

The Revere Mobile platform uses a REST architecture. All requests to the platform must set the Content-Type and Accept HTTP headers to application/json. While the platform can accept calls over the HTTP or HTTPS protocol, by default, you should use the HTTPS protocol. When you authenticate a session, the response will set two cookies: SessionId and JSESSIONID. You must include these cookies in all subsequent requests, they identify your authenticated session. All the examples below include HTTP headers and payload for requests and responses as given by curl.

#### Example 1: Logging in and out

** To authenticate a session **

To start an authenticated session, call the v1/authenticate method, using the username and password associated with your account.

Send a POST request to https://revolutionmsg.com/v1/authenticate. The JSON request payload has the following format, where username and password are your username and password.

HTTP Request:

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

HTTP Response:

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
  
On successful authentication, the response has a status code of 200 (OK), a null payload, and the response sets the SessionId and JSESSIONID cookies, which identifies your session.

** To check session status **

Your session remains authenticated for up to 30 minutes of idle time. You can call the v1/authenticate/whoami method to check the current session status.

Send a GET request to https://revolutionmsg.com/v1/authenticate/whoami
If your session is still authenticated, the response has a status code of 200 (OK), and the response payload contains information about your session.

HTTP Request:

    GET /v1/authenticate/whoami HTTP/1.1
    User-Agent: curl/7.30.0
    Host: revolutionmsg.com
    Cookie: SessionId=0d9f43c7-dee6-4297-b555-c25f13b496b2; JSESSIONID=0d9f43c7-dee6-4297-b555-c25f13b496b2
    Accept:application/json
HTTP Response:

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
  
Otherwise, the response has a status code of 401 (Unauthorized).

** To actively close a session **

Whenever you are finished accessing the platform, you should actively log out.

Send a POST request with null payload to https://revolutionmsg.com/v1/authenticate/logout
#### Example 2: Sending an SMS message

You can send a simple, one-off message to a subscriber by using the v2/message method.

Start with an authenticated session, as described in the Example 1: Logging in and out section.
Send a POST request to https://revolutionmsg.com/api/v2/message. Include a JSON request payload with the following format, where number is the mobile number to which to send the message, and message is the message to send.

HTTP Request

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
HTTP Response

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
  
#### Example 3: Subscribe an end user to a list and add metadata for the user

This example demonstrates how to create a list and metadata field, join a subscriber to that list and update the metadata field for that subscriber, and then verify the operation by getting the profile of the subscriber.

Start with an authenticated session, as described in the Example 1: Logging in and out section.
Send a POST request to https://revolutionmsg.com/v1/list to create a list to which to add the subscriber. Make a note of the list ID, which is contained in the response payload.

HTTP Request

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

HTTP Response

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
  
Send a POST request to https://revolutionmsg.com/v1/metadata to create the metadata field. Make a note of the metadata ID, which is contained in the response payload.
HTTP Request

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
  
HTTP Response

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
  
Send a POST request to https://revolutionmsg.com/v1/messaging/sendContent endpoint to send a sequence of content modules to the subscriber. The first module will add the subscriber to the list created in step 2. The second module will update the value of the metadata field you created in step 3. In the request payload, update the appropriate fields with the IDs from previous steps.
* Set `msisdns` to the phone number(s) of the subscriber(s) you wish to add to your list.
* Set `listId` to the ID of the list from step 2.
* Set `subscribedMessage` to the message to send the subscriber if they are already a member of the list. This element can be omitted if you do not want to send a message.
* Set `confirmedMessage` to the message to send the subscriber if they are successfully added to the list. This element can be omitted if you do not want to send a confirmation message.
* Set `metadataFieldId` to the ID of the metadata field from step 3.
* Replace My Tag with the value to assign to this field for this subscriber.

HTTP Request

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
  
HTTP Response

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
  
The subscriber receives the confirmed or subscribed message from the short code associated with the session from which the message was initiated.

Send a GET request to https://revolutionmsg.com/v1/subscriber/{id_or_msisdn} endpoint to verify that the subscriber is joined to the list and their metadata field has been updated. Replace the {id_or_msisdn} PATH parameter with the mobile phone number of the subscriber for which you wish to retrieve data.

HTTP Request

    POST /v1/subsriber/12024561414 HTTP/1.1
    User-Agent: curl/7.30.0
    Host: revolutionmsg.com
    Cookie: SessionId=ee2fdf0a-96ae-43d1-8315-74626215adbd; JSESSIONID=ee2fdf0a-96ae-43d1-8315-74626215adbd
    Content-Type:application/json
    Accept:application/json
    Content-Length: 0  
  
HTTP Response

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
