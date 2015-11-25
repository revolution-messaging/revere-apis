# API

This describes the resources that make up the official Revere Exchange API v1. If you have any problems or requests please contact [Josh Minnich](mailto: josh@revolutionmessaging.com) or [Walker Hamilton](mailto: walker@revolutionmessaging.com).

- [Current Version](#current-version)
- [Schema](#schema)
- [Base Endpoint](#base-endpoint)
- [Sessions (Authentication)](#sessions-authentication)
- [Audiences](#audiences)
- [Ads (Advertisements)](#ads-advertisements)
- [Campaigns](#campaigns)
- [Clients](#clients)
- [Uploads (Attachments)](#uploads-attachments)

### Current Version

By default, all requests receive the v1 version of the API. We encourage you to explicitly request this version via the Accept header.

```
Accept: application/vnd.revere-exchange-v1+json
```

### Schema

All API access is over HTTPS, and accessed from the xchng.reverehq.com domain. All data is sent and received as JSON unless otherwise noted.

```
HTTP/1.1 200 OK
Server: Cowboy
Date: Mon, 21 Sep 2015 18:06:01 GMT
Connection: close
Content-Type: application/json
Vary: Origin
Etag: W/"0c776997933eb60833b37beaf43814c8"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: f0727bbf-f4ca-46d0-8bd5-16911ea95457
X-Runtime: 1.000175
Content-Length: 15
Via: 1.1 vegur

{"status":"OK"}
```

### Base Endpoint

Production

```
https://xchng.reverehq.com/api
```

Staging

```
https://xchngstaging.reverehq.com/api
```

### Sessions (Authentication)

#### Create a session

```
POST /sessions
```

**Request**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| id | Integer | True | Value of `revere` cookie from Dashboard (Revere SSO) |
| session | String | True | Value of `revere_session` cookie from Dashboard (Revere SSO) |

```json
{
  "id": "1",
  "session": "d59c5a2eb1058dd4fb04122a428b139e94315d7791e07326198d5ff028d4a5ffe9cd289ffcb059a2"
}
```

**Response**

```json
{
  "sso_uid": "4879d096-76a1-4618-aa8e-2a7c93e79428",
  "email": "josh@revolutionmessaging.com",
  "auth_token": "[filtered]",
  "user": {
    "id": 1,
    "name": "Josh Minnich",
    "role": "admin"
  }
}
```

### Audiences

Audiences are required to have an attached list file associated. To attach a file to an audience you must first upload a file through the [uploads endpoint](#uploads-attachments) and set the required audience fields to the response of the uploaded attachment.

#### List audiences

```
GET /audiences?page=&per_page=&offset=
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| page | Integer | False | Current page (default: 1) |
| per_page | Integer | False | How many to list in a page (default: 25) |
| offset | Integer | False | The offset to start from (default: 0) |

**Response**

```json
{
  "audiences": [
    {
      "id": 1,
      "status": "active",
      "name": "My cool audience",
      "list_url": "https://revere-exchange.s3.amazonaws.com/audiences/2015/a861251e8269639dbadd36693f524bb8/my_cool_audience.csv",
      "list_file_name": "/audiences/2015/a861251e8269639dbadd36693f524bb8/my_cool_audience.csv",
      "list_file_size": 1024,
      "list_content_type": "text/csv",
      "list_updated_at": "2015-09-21T22:49:43-07:00",
      "created_at": "2015-09-20T19:50:15-07:00",
      "updated_at": "2015-09-20T19:50:15-07:00"
    }
  ]
}
```

#### Get a single audience

```
GET /audiences/:audience_id
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| audience_id | Integer | True | ID for audience record |

**Response**

```json
{
  "audience": {
    "id": 1,
    "status": "active",
    "name": "My cool audience",
    "list_url": "https://revere-exchange.s3.amazonaws.com/audiences/2015/a861251e8269639dbadd36693f524bb8/my_cool_audience.csv",
    "list_file_name": "/audiences/2015/a861251e8269639dbadd36693f524bb8/my_cool_audience.csv",
    "list_file_size": 1024,
    "list_content_type": "text/csv",
    "list_updated_at": "2015-09-21T22:49:43-07:00",
    "created_at": "2015-09-20T19:50:15-07:00",
    "updated_at": "2015-09-20T19:50:15-07:00"
  }
}
```

#### Create an audience

```
POST /audiences
```

**Request**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| name | String | True | Name of audience |
| list_file_name | String | True | File name (key) from uploaded attachment |
| list_file_size | Integer | True | Size of uploaded attachment in bytes |
| list_content_type | String | True | Mime-type of uploaded attachment |

```json
{
  "audience": {
    "name": "My even cooler audience",
    "list_file_name": "/audiences/2015/5a837fed24dd1897978362b45bec887c/my_even_cooler_audience.csv",
    "list_file_size": 2048,
    "list_content_type": "text/csv"
  }
}
```

**Response**

```json
{
  "audience": {
    "id": 2,
    "status": "active",
    "name": "My even cooler audience",
    "list_url": "https://revere-exchange.s3.amazonaws.com/audiences/2015/5a837fed24dd1897978362b45bec887c/my_even_cooler_audience.csv",
    "list_file_name": "/audiences/2015/5a837fed24dd1897978362b45bec887c/my_even_cooler_audience.csv",
    "list_file_size": 2048,
    "list_content_type": "text/csv",
    "list_updated_at": "2015-09-22T22:49:43-07:00",
    "created_at": "2015-09-21T19:50:15-07:00",
    "updated_at": "2015-09-21T19:50:15-07:00"
  }
}
```

#### Update an audience

```
PUT /audiences/:audience_id
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| audience_id | Integer | True | ID for audience record |

**Request**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| name | String | False | Name of audience |
| status | String | False | Status of audience (active, suspended, closed) |
| list_file_name | String | False | File name (key) from uploaded attachment |
| list_file_size | Integer | If given **list_file_name** | Size of uploaded attachment in bytes |
| list_content_type | String | If given **list_file_name** | Mime-type of uploaded attachment |

```json
{
  "audience": {
    "list_file_name": "/audiences/2015/5a837fed24dd1897978362b45bec887c/corrected_audience.csv",
    "list_file_size": 1037,
    "list_content_type": "text/csv"
  }
}
```

**Response**

```json
{
  "audience": {
    "id": 2,
    "status": "active",
    "name": "My even cooler audience",
    "list_url": "https://revere-exchange.s3.amazonaws.com/audiences/2015/5a837fed24dd1897978362b45bec887c/corrected_audience.csv",
    "list_file_name": "/audiences/2015/5a837fed24dd1897978362b45bec887c/corrected_audience.csv",
    "list_file_size": 1037,
    "list_content_type": "text/csv",
    "list_updated_at": "2015-09-22T22:49:43-07:00",
    "created_at": "2015-09-21T19:50:15-07:00",
    "updated_at": "2015-09-21T19:50:15-07:00"
  }
}
```

#### Delete an audience

The record for the audience is not deleted. Instead the record is marked as suspended in the database. The audience can be re-activated by using the update endpoint and setting the status to active.

```
DELETE /audiences/:audience_id
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| audience_id | Integer | True | ID for audience record |

**Response**

```
Status: 202 (Accepted)
```

### Ads (Advertisements)

To attach a file to an advertisement you must first upload a file through the [uploads endpoint](#uploads-attachments) and set the required advertisement fields to the response of the uploaded attachment.

#### List ads

```
GET /clients/:client_id/ads?page=&per_page=&offset=
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| client_id | Integer | True | ID for the client record the ads belong to |
| page | Integer | False | Current page (default: 1) |
| per_page | Integer | False | How many to list in a page (default: 25) |
| offset | Integer | False | The offset to start from (default: 0) |

**Response**

```json
{
  "ads": [
    {
      "id": 1,
      "status": "active",
      "name": "Video Advertisement",
      "media_url": "https://revere-exchange.s3.amazonaws.com/ads/2015/a4d704d3e280a8e3a11d002145cf523b/video_advertisement.mp4",
      "media_file_name": "video_advertisement.mp4",
      "media_file_size": 23437,
      "media_content_type": "video/mp4",
      "media_updated_at": "2015-09-21T22:49:43-07:00",
      "created_at": "2015-09-20T19:50:15-07:00",
      "updated_at": "2015-09-20T19:50:15-07:00"
    }
  ]
}
```

#### Get a single ad

```
GET /clients/:client_id/ads/:ad_id
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| client_id | Integer | True | ID for the client record the ad belongs to |
| ad_id | Integer | True | ID for ad record |

**Response**

```json
{
  "ad": {
    "id": 1,
    "status": "active",
    "name": "Video Advertisement",
    "media_url": "https://revere-exchange.s3.amazonaws.com/ads/2015/a4d704d3e280a8e3a11d002145cf523b/video_advertisement.mp4",
    "media_file_name": "video_advertisement.mp4",
    "media_file_size": 23437,
    "media_content_type": "video/mp4",
    "media_updated_at": "2015-09-21T22:49:43-07:00",
    "created_at": "2015-09-20T19:50:15-07:00",
    "updated_at": "2015-09-20T19:50:15-07:00"
  }
}
```

#### Create an ad

```
POST /clients/:client_id/ads
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| client_id | Integer | True | ID for the client record the ad belongs to |

**Request**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| name | String | True | Name of advertisement |
| media_type | String | True | Type of advertisement |
| media_file_name | Integer | False | File name (key) from uploaded attachment |
| media_file_size | String | If given **media_file_name** | Size of uploaded attachment in bytes |
| media_content_type | String | If given **media_file_name** | Mime-type of uploaded attachment |

```json
{
  "ad": {
    "name": "Display Ad",
    "media_type": "adDisplay",
    "media_file_name": "cool_image.jpg",
    "media_file_size": 128,
    "media_content_type": "image/jpg"
  }
}
```

**Response**

```json
{
  "ad": {
    "id": 2,
    "status": "active",
    "name": "Display Ad",
    "media_type": "adDisplay",
    "media_url": "https://revere-exchange.s3.amazonaws.com/ads/2015/ee2c55a90afb289207d89ca2fda1f8fd/cool_image.jpg",
    "media_file_name": "cool_image.jpg",
    "media_file_size": 128,
    "media_content_type": "image/jpg",
    "media_updated_at": "2015-09-22T22:49:43-07:00",
    "created_at": "2015-09-21T19:50:15-07:00",
    "updated_at": "2015-09-21T19:50:15-07:00"
  }
}
```

#### Update an ad

```
PUT /clients/:client_id/ads/:ad_id
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| client_id | Integer | True | ID for the client record the ad belongs to |
| ad_id | Integer | True | ID for ad record |

**Request**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| name | String | True | Name of advertisement |
| status | String | False | Status of advertisement (active, suspended, closed) |
| media_type | String | True | Type of advertisement |
| media_file_name | Integer | False | File name (key) from uploaded attachment |
| media_file_size | String | If given **media_file_name** | Size of uploaded attachment in bytes |
| media_content_type | String | If given **media_file_name** | Mime-type of uploaded attachment |

```json
{
  "ad": {
    "name": "Better Name"
  }
}
```

**Response**

```json
{
  "ad": {
    "id": 2,
    "status": "active",
    "name": "Better Name",
    "media_type": "adDisplay",
    "media_url": "https://revere-exchange.s3.amazonaws.com/ads/2015/ee2c55a90afb289207d89ca2fda1f8fd/cool_image.jpg",
    "media_file_name": "cool_image.jpg",
    "media_file_size": 128,
    "media_content_type": "image/jpg",
    "media_updated_at": "2015-09-22T22:49:43-07:00",
    "created_at": "2015-09-21T19:50:15-07:00",
    "updated_at": "2015-09-21T19:50:15-07:00"
  }
}
```

#### Delete an ad

The record for the advertisement is not deleted. Instead the record is marked as suspended in the database. The advertisement can be re-activated by using the update endpoint and setting the status to active.

```
DELETE /clients/:client_id/ads/:ad_id
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| client_id | Integer | True | ID for the client record the ad belongs to |
| ad_id | Integer | True | ID for ad record |

**Response**

```
Status: 202 (Accepted)
```

### Campaigns

Campaigns have a complex relationship between audiences and advertisements. Campaigns don't the relationships, they reference the different models. This means that campaigns can reference multiple audience and advertisement relationships and the individual audiences and advertisements can work independently on their own. Check out the [create a campaign](#create-a-campaign) section below to see how the relationships work.

#### List campaigns

```
GET /clients/:client_id/campaigns
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| client_id | Integer | True | ID for the client record the campaign belongs to |

**Response**

```json
{
  "campaigns": [
    {
      "id": 1,
      "client_id": 1,
      "status": "active",
      "name": "Why team dog is better",
      "goal": "awareness",
      "budget": "700.25",
      "start_date": "2015-09-23T11:40:05-07:00",
      "end_date": "2015-10-23T11:40:05-07:00"
    }
  ]
}
```

#### Get a single campaign

```
GET /clients/:client_id/campaigns/:campaign_id
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| client_id | Integer | True | ID for the client record the campaign belongs to |
| campaign_id | Integer | True | ID for campaign record |

**Response**

```json
{
  "campaigns": {
    "id": 1,
    "client_id": 1,
    "status": "active",
    "name": "Why team dog is better",
    "goal": "awareness",
    "budget": "700.25",
    "start_date": "2015-09-23T11:40:05-07:00",
    "end_date": "2015-10-23T11:40:05-07:00",
    "audiences": [
      {
        "id": 1,
        "name": "Team Dog",
        "status": "active",
        "list_file_name": "/audiences/2015/5a837fed24dd1897978362b45bec887c/team_dog.csv",
        "list_file_size": "2752",
        "list_content_type": "text/csv",
        "list_url": "https://revere-exchange.s3.amazonaws.com/audiences/2015/5a837fed24dd1897978362b45bec887c/team_dog.csv",
        "list_updated_at": "2015-09-22T22:49:43-07:00",
        "created_at": "2015-09-22T22:49:43-07:00",
        "updated_at": "2015-09-22T22:49:43-07:00"
      }
    ],
    "advertisements": [
      {
        "id": 1,
        "name": "Team Dog Video",
        "status": "active",
        "media_type": "adVideo",
        "media_url": "https://revere-exchange.s3.amazonaws.com/ads/2015/ee2c55a90afb289207d89ca2fda1f8fd/team_dog_video.mp4",
        "media_file_name": "/ads/2015/ee2c55a90afb289207d89ca2fda1f8fd/team_dog_video.mp4",
        "media_file_size": 5120,
        "media_content_type": "video/mp4",
        "media_updated_at": "2015-09-22T22:49:43-07:00",
        "created_at": "2015-09-21T19:50:15-07:00",
        "updated_at": "2015-09-21T19:50:15-07:00"
      }
    ],
    "created_at": "2015-09-21T19:50:15-07:00",
    "updated_at": "2015-09-21T19:50:15-07:00"
  }
}
```

#### Create a Campaign

```
POST /clients/:client_id/campaigns
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| client_id | Integer | True | ID for the client record the campaign belongs to |

**Request**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| name | String | True | Name of campaign |
| goal | String | True | Goal of campaign (awareness, acquisition) |
| start_date | Integer | True | Start date and time of campaign |
| end_date | String | True | End date and time of campaign |
| ad_ids | Int[] | False | Array of Ad IDs to associate with the campaign |
| ads_campaigns_attributes | Object[] | False | Array of Ad objects to create and associate with the campaign |
| audience_ids | Int[] | False | Array of Audience IDs to associate with the campaign |
| audiences_campaigns_attributes | Object[] | False | Array of Ad objects to create and associate with the campaign |

```json
{
  "campaigns": {
    "name": "Go Team Dog",
    "goal": "acquisition",
    "budget": "1200.00",
    "start_date": "2015-09-23T11:40:05-07:00",
    "end_date": "2015-10-23T11:40:05-07:00",
    "audiences_campaigns_attributes": [
      {
        "audience_attributes": {
          "name": "Team Cat",
          "list_file_name": "/audiences/2015/5a837fed24dd1897978362b45bec887c/team_cat.csv",
          "list_file_size": "800",
          "list_content_type": "text/csv",
          "list_updated_at": "2015-09-22T22:49:43-07:00"
        }
      }
    ],
    "ads_campaigns_attributes": [
      {
        "saturation": "high",
        "ad_attributes": {
          "client_id": 1,
          "name": "Go Team Dog Hooray Hooray",
          "media_type": "adVideo",
          "media_file_name": "/ads/2015/ee2c55a90afb289207d89ca2fda1f8fd/go_team_dog_hooray_hooray.mp4",
          "media_file_size": 5120,
          "media_content_type": "video/mp4",
          "media_updated_at": "2015-09-22T22:49:43-07:00"
        }
      }
    ]
  }
}
```

**Response**

```json
{
  "campaigns": {
    "id": 2,
    "name": "Go Team Dog",
    "goal": "acquisition",
    "budget": "1200.00",
    "start_date": "2015-09-23T11:40:05-07:00",
    "end_date": "2015-10-23T11:40:05-07:00",
    "audiences": [
      {
        "id": 2,
        "name": "Team Cat",
        "list_file_name": "/audiences/2015/5a837fed24dd1897978362b45bec887c/team_cat.csv",
        "list_file_size": "800",
        "list_content_type": "text/csv",
        "list_updated_at": "2015-09-22T22:49:43-07:00"
      }
    ],
    "ads": [
      {
        "id": 2,
        "client_id": 1,
        "saturation": "high",
        "name": "Go Team Dog Hooray Hooray",
        "media_type": "adVideo",
        "media_file_name": "/ads/2015/ee2c55a90afb289207d89ca2fda1f8fd/go_team_dog_hooray_hooray.mp4",
        "media_file_size": 5120,
        "media_content_type": "video/mp4",
        "media_updated_at": "2015-09-22T22:49:43-07:00"
      }
    ]
  }
}
```

#### Update a Campaign

```
PUT /clients/:client_id/campaigns/:campaign_id
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| client_id | Integer | True | ID for the client record the campaign belongs to |
| campaign_id | Integer | True | ID for campaign record |

**Request**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| name | String | False | Name of campaign |
| status | String | False | Status of campaign (active, suspended, closed) |
| goal | String | False | Goal of campaign (awareness, acquisition) |
| start_date | Integer | False | Start date and time of campaign |
| end_date | String | False | End date and time of campaign |
| ad_ids | Int[] | False | Array of Ad IDs to associate with the campaign |
| ads_campaigns_attributes | Object[] | False | Array of Ad objects to create and associate with the campaign |
| audience_ids | Int[] | False | Array of Audience IDs to associate with the campaign |
| audiences_campaigns_attributes | Object[] | False | Array of Ad objects to create and associate with the campaign |

```json
{
  "campaigns": {
    "budget": "2000.00",
  }
}
```

**Response**

```json
{
  "campaigns": {
    "id": 2,
    "name": "Go Team Dog",
    "goal": "acquisition",
    "budget": "2000.00",
    "start_date": "2015-09-23T11:40:05-07:00",
    "end_date": "2015-10-23T11:40:05-07:00",
    "audiences": [
      {
        "id": 2,
        "name": "Team Cat",
        "list_file_name": "/audiences/2015/5a837fed24dd1897978362b45bec887c/team_cat.csv",
        "list_file_size": "800",
        "list_content_type": "text/csv",
        "list_updated_at": "2015-09-22T22:49:43-07:00"
      }
    ],
    "ads": [
      {
        "id": 2,
        "client_id": 1,
        "saturation": "high",
        "name": "Go Team Dog Hooray Hooray",
        "media_type": "adVideo",
        "media_file_name": "/ads/2015/ee2c55a90afb289207d89ca2fda1f8fd/go_team_dog_hooray_hooray.mp4",
        "media_file_size": 5120,
        "media_content_type": "video/mp4",
        "media_updated_at": "2015-09-22T22:49:43-07:00"
      }
    ]
  }
}
```

#### Delete a Campaign

The record for the campaign is not deleted. Instead the record is marked as suspended in the database. The campaign can be re-activated by using the update endpoint and setting the status to active.

```
DELETE /clients/:client_id/campaigns/:campaign_id
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| client_id | Integer | True | ID for the client record the campaign belongs to |
| campaign_id | Integer | True | ID for campaign record |

**Response**

```
Status: 202 (Accepted)
```

### Clients

#### List clients

```
GET /clients
```

**Response**

```json
{
  "clients": [
    {
      "id": 1,
      "status": "active",
      "sso_id": 11,
      "name": "The Blue Toed Socks",
      "created_at": "2015-09-21T17:51:29-05:00",
      "updated_at": "2015-09-21T17:51:29-05:00"
    }
  ]
}
```

Get a single client

```
GET /clients/:client_id
```

**Parameters**

| Name | Type | Required | Description |
| ---- | ---- | -------- | ----------- |
| client_id | Integer | True | ID for client record |

**Response**

```json
{
  "client": {
    "id": 1,
    "status": "active",
    "sso_id": 11,
    "name": "The Blue Toed Socks",
    "created_at": "2015-09-21T17:51:29-05:00",
    "updated_at": "2015-09-21T17:51:29-05:00"
  }
}
```

### Uploads (Attachments)

Returns a URL to upload and pre-signed post fields that need to be sent along to the URL for direct uploading. For more information about direct uploading to S3 check out the [Direct to S3 Image Uploads in Rails](https://devcenter.heroku.com/articles/direct-to-s3-image-uploads-in-rails) article posted at the Heroku Dev Center.

#### Get a new upload

```
GET /uploads/new?type=ad|audience
```

**Parameters**

| Name | Type | Required | Description | Allowed values |
| ---- | ---- | -------- | ----------- | -------------- |
| type | String | True | Type of attachment to create | ad, audience |

**Response**

```json
{
  "url": "https://revere-exchange.s3.amazonaws.com",
  "fields": {
    "acl": "public-read",
    "key": "ads/2015/${filename}",
    "policy": "eyJleHBpcmF0aW9uIjoiMjAxNS0wOS0yMlQxNzo0NToyNloiLCJjb25kaXRpb25zIjpbeyJidWNrZXQiOiJyZXZlcmUtZXhjaGFuZ2UifSx7ImFjbCI6InB1YmxpYy1yZWFkIn0sWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJhZHMvMjAxNS8iXSx7IngtYW16LWNyZWRlbnRpYWwiOiJBS0lBSVI1UERSVUJSWjdYVjIyUS8yMDE1MDkyMi91cy1lYXN0LTEvczMvYXdzNF9yZXF1ZXN0In0seyJ4LWFtei1hbGdvcml0aG0iOiJBV1M0LUhNQUMtU0hBMjU2In0seyJ4LWFtei1kYXRlIjoiMjAxNTA5MjJUMTY0NjAwWiJ9XX0=",
    "x-amz-credential": "AKIAIR5PDRUBRZ7XV22Q/20150922/us-east-1/s3/aws4_request",
    "x-amz-algorithm": "AWS4-HMAC-SHA256",
    "x-amz-date": "20150922T164600Z",
    "x-amz-signature": "510581c867cfd65650c0ff9c87c4b05adf4cc5bad0dc4c95ecdeb2354070e081"
  }
}
```
