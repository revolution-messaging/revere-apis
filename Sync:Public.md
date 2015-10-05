# Sync: Public
---
HOST: https://sync.revmsg.net

An API from Revolution Messaging, LLC. This API is used to submit public requests via https to Sync. Generally, these requests are publicly initiated via a client browser.

Copyright (c) 2013 Revolution Messaging, LLC

HTTP Response Codes
---
- 202 `Accepted` - The request will be processed asynchronously.
- 400 `Bad Request` - The request could not be interpreted correctly or some required parameters were missing.
- 401 `Unauthorized` - Authentication failed - double-check your username and/or password.
- 405 `Method Not Allowed` - The requested method is not supported. Only GET and POST are allowed.
- 429 `Too Many Requests` - Quota or rate limit exceeded.
- 500 `Internal Server Error` - Something is broken. Please contact us and we'll investigate.

---

### Constituents

Public constituent queueing methods.

**Parameters:**
```
GET /constituent/{passkey}
```
* `misc` (optional) - You can provide any other variable name in the place of "misc" and this will be saved and available data for that constituent.
* `services` = "mobilize" (optional, string) - Multiples of this parameter can be provided in a single request.
* `ask` (optional) - String to tag request with. This is for tracking which ask this use responded to. Multiples of this parameter can be provided in a single request.
* `tags` (optional, string) - String to tag request with. This tag can be used to note affiliations & to filter triggers. Multiples of this parameter can be provided in a single request.
* `occupation` (optional, string) - Constituent's occupation
* `employer` (optional, string) - Constituent's employer.
* `zip` (optional, string) - Constituent's zip code in 5-digit, 9-digit, or 10-character format. 10 accounting for the dash between the zip and the "plus-four".
* `state` (optional, string) - Constituent's state in ISO 3166-2:US format
* `city` (optional, string) - Constituent's city.
* `unit` (optional, string) - Line two of the constituent's address.
* `address` (optional, string) - Line one of the constituent's address.
* `lastname` (optional, string) - Constituent's lastname
* `firstname` (optional, string) - Constituent's firstname
* `name` (optional, string) - Constituent's name. No formatting rules. If one word provided, assumes firstname. If more, splits out to first/middle(s)/last
* `phone` (optional, string) - Phone number in any format. Put phone number in E164 format if at all possible. You must provide either this or email to make the request valid.
* `email` (optional, string) - You must provide either this or phone number to make the request valid. Multiples of this parameter can be provided in a single request.
* `passkey` (required, string) - A hash string that provides control and submit connection for an account.

**Response:**
```
Status: 202 (Accepted)
```

**Request fields:**
```
POST /constituent/{passkey}
```
* `passkey` (required, string) - A hash string that provides control and submit connection for an account.
* `name` (optional, string) - Constituent's name. No formatting rules. If one word provided, assumes firstname. If more, splits out to first/middle(s)/last
* `firstname` (optional, string) - Constituent's firstname
* `lastname` (optional, string) - Constituent's lastname
* `email` (optional, string) - You must provide either this or phone number to make the request valid. Multiples of this parameter can be provided in a single request.
* `phone` (optional, string) - Phone number in any format. Put phone number in E164 format if at all possible. You must provide either this or email to make the request valid.
* `address` (optional, string) - Line one of the constituent's address.
* `unit` (optional, string) - Line two of the constituent's address.
* `city` (optional, string) - Constituent's city.
* `state` (optional, string) - Constituent's state in ISO 3166-2:US format
* `zip` (optional, string) - Constituent's zip code in 5-digit, 9-digit, or 10-character format. 10 accounting for the dash between the zip and the "plus-four".
* `employer` (optional, string) - Constituent's employer.
* `occupation` (optional, string) - Constituent's occupation
* `tags` (optional, string) - String to tag request with. This tag can be used to note affiliations & to filter triggers. Multiples of this parameter can be provided in a single request by using a comma-delimited string or providing multiple tags= items in the querystring.
* `ask` (optional) - String to tag request with. This is for tracking which ask this use responded to. Multiples of this parameter can be provided in a single request by using a comma-delimited string or providing multiple ask= items in the querystring.
* `services` = "mobilize" (optional, string) - Multiples of this parameter can be provided in a single request by using a comma-delimited string or providing multiple services= items in the querystring.
* `misc` (optional) - You can provide any other variable name in the place of "misc" and this will be saved and available data for that constituent.

**Response:**
```
Status: 202 (Accepted)
```

**Parameters:**
```
PUT /constituent/{passkey}
```
* passkey (required, string) - A hash string that provides control and submit connection for an account.

**Response:**
```
Status: 202 (Accepted)
```

--
### Actions

Public action queueing method.
```
POST /action/{passkey}
```
Record an action. You must provide `type` & one of these: `constituentID`, `email`, or `phone`

* `passkey` (required, string) - A hash string that provides control and submit connection for an account.
* `constituentID` (optional, string) - Unique identifier for constituent to associate with action undertaken.
* `email` (optional, string) - Email address to associate with action undertaken by constituent.
* `phone` (optional, string) - Phone number to associate with action undertake by constituent.
* `data` (optional, array) - A key value array of any necessary data for the particular action taken.
* `source` (optional, string) - Name, title, unique identifier or description of the application, site, url, flyer that initiated this action.
* `method` (optional, string) - Media via which this action was undertaken. If "share" then use as string to describe platform. If call then use ""
* `type` (required, string) - Can be one of these: call, text, poll, donation, petition, share

For `type=call`, the `data` object should look something like this:
```
{
  length: "00:00", (length of user's call)
  connected_to: { (provide one or more of the following)
      lz_api_id: "", (uuid of lz legislator)
      legislator_name: "", (legislator name)
      phone: "" (phone number connected to)
  }
}
``` 
