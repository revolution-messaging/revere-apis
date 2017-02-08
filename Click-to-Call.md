# Click-to-Call

An API from Revolution Messaging, LLC. Click-to-Call is a RevereCalling API that allows you to trigger a call from your calling campaign line on a website, social network, or via other means.

HOST: https://phone.reverehq.com/

Copyright (c) 2017 Revolution Messaging, LLC

*_Please note_: We will close down any account found to be triggering calls using methods beyond intentional user interaction.*

## Details

Outbound click-to-call accepts via GET & POST. Both GET & POST amount to the same action.

If the "revmsghtml" parameter is provided, there is no callback in the URL, and the Content-Type header indicates that the browser submitted the request, then the system should redirect to that fully-qualified URL with a 302, no matter the outcome of the request.

## Returned error messages

If there was a problem placing the phone call you will recieve a status code of 400 with one of the following error messages in the returned payload:

* If the required parameters were not provided or were not in the proper format: _Sorry, but you haven't provided any of the info we were expecting._
* If the provided campaign line is not found in the system: _This phone number is not configured._
* If there was any other error: _Sorry, there was an error._

## Click-to-Call

### Initiate call

```
GET /outgoing
```

Returns json if json in Accept header, or a callback-wrapped json object if JSONP is specified and a callback variable is provided. See _details_, above, for special redirect cases.

#### Parameters

- *phone* (required, string) - The phone number that is to be called by the service (usually supplied by the constituent).
- *campaign_line* (required, string) - The phone number for the campaign for which the call should be triggered.
- *name* (optional, string) - The constituent's name.
- *email* (optional, string) - The constituent's email address.
- *revmsghtml* (optional, string) - A fully-qualified URL that the system can redirect to if the request is made using text/html or text/plain content-types.
- *data* (optional, string) - A valid string-encoded json object with variables that can be loaded later in the call.

#### Response 200

```
{
  "error":false,
  "message": "The call's been placed."
}
```

### Initiate call

```
POST /outgoing
```

Returns json if json in Accept header, or a callback-wrapped json object if JSONP is specified and a callback variable is provided. See _details_, above, for special redirect cases.

#### Parameters

These request parameters can be provided via POST using: application/json, application/x-www-form-urlencoded, or in the URL querystring.

- *phone* (required, string) - The phone number that is to be called by the service (usually supplied by the constituent).
- *campaign_line* (required, string) - The phone number for the campaign for which the call should be triggered.
- *name* (optional, string) - The constituent's name.
- *email* (optional, string) - The constituent's email address.
- *revmsghtml* (optional, string) - A fully-qualified URL that the system can redirect to if the request is made using text/html or text/plain content-types.
- *data* (optional, json) - A valid json object with variables that can be loaded later in the call.

#### Request

```json
{
  "phone": "(617) 523-2338",
  "campaign_line": "+13213214321",
  "name": "Paul Revere",
  "email": "paul.revere@revolutionmessaging.com",
  "zip":"02113"
}
```

#### Response 200

```
{
  "error": false,
  "message": "The call's been placed."
}
```
