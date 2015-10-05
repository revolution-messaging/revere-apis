# Revere Direction
Revere Direction is a URL shortener service similar to bit.ly enterprise.

Base API URL: https://direction.reverehq.com/api/v1

## [Links](/link?access_token={access_token})

**Parameters**
* access_token (required, string) ... String access token connected to your account.

### Create a New Short URL [POST]
**Request**
```json
{ "url": "http://shortenthisdomainlink.com/shorter/please", "slug": "", "notes": "" }
```
**Response**
```json
Status: 201 

{ "id": 3, "title": "Buy cheese and bread for breakfast." }
```

## [Desktop v. Mobile Stats for Link](/stats/{id}/desktop_mobile)
A single link object with its desktop versus mobile stats

**Parameters**
+ id (required, number, `1`) ... Numeric `id` of the short URL to get stats for. Has example value.

## Desktop v. Mobile Stats for Link [GET]
**Response**
```json
Status: 200 
```
+ Header
```
X-My-Header: The Value
```
+ Body
```json
{ "id": 2, "title": "Pick-up posters from post-office" }
```
