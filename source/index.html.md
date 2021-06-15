---
title: Evanta API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - ruby

toc_footers:
  - VERSION 1.0.1
  - © 2019. All rights reserved.

search: true
---

# Getting Started

Welcome to the Evanta Registration API for Validar.

The information contained here will help you get started, and the menu on the left will show you the specifics about submitting and retrieving data from our system. The information on the right will show you the curl commands and responses.

## Authentication
> To authorize, use this code:

```shell
curl 'https://eventbeyondapi.emt.aws.gartner.com/validar/registrations/event/<EVENT_CODE>' -H 'Authorization: Token token="<TOKEN>"' -H 'X_API_TENANT: evantaconnect' -H 'Accept: application/json, text/javascript, /; q=0.01' -H 'X_API_EMAIL: validar.api.user@evanta.com'
```

First things first, you must have permission to access to the public API, and that permission is granted through your Validar Admin Role.

Once you have successfully authenticated and can retrieve some information, you are ready to dig a little deeper. Check out the menu on the left for specifics about registrations.

<aside class="notice">
  You must replace <code>TOKEN</code> with your personal API key and <code>EVENT_CODE</code> with the event code you are after.
</aside>

# Registrations

A registration is made up of the following attributes:

Attribute | Type | Required | Notes
---:|:---:|:---:|:---
**id** | integer | ✔️ |  Your unique identifier
**event_code** | string | ✔️ | Evanta event unique identifier
**attendee_type** | string | | "Attendee" or "Sponsor"
**first_name** | string |✔️ |
**last_name** | string | ✔️|
**title** | string | |
**organization_name** | string | |
**email** | string |✔️ |
**status** | string | | "Approved" or "Sponsor Approved"
**last_modified_date_time** | datetime | |
**event_hub_link**  | string | | Validar field
**event_hub_pk_pass_link** | string | | Validar field
**event_hub_qr_code_link** | string | | Validar field
**event_ext_value_01** | string | | Evanta QR Code value
**event_ext_value_02** | string | | Ribbon value: "Speaker"
**event_ext_value_03** | string | | Ribbon value: "Governing Body" or "Chair"
**is_attended** | boolean | | true, "true", or 1 for **True**
|||false, "false", or 0 for **False**


## Get All Registrations

```shell
  curl "http://eventbeyondapi.emt.aws.gartner.com/validar/registrations/event/<EVENT_CODE>?since_datetime='2018-12-19 01:22:42'"
  -H 'Authorization: Token token="<TOKEN>"'
  -H 'X_API_TENANT: evantaconnect'
  -H 'Accept: application/json, text/javascript, /; q=0.01'
  -H 'X_API_EMAIL: validar.api.user@evanta.com'
```
```ruby
require 'uri'
require 'net/http'

url = URI("http://localhost:3000/validar/registrations/event/18EVAPRAPR01")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Token token="BZIpRazA3KqrQaNOMqiOJQ"'
request["X_API_EMAIL"] = 'validar.api.user@evanta.com'
request["X-API-Tenant"] = 'evantaconnect'
request["cache-control"] = 'no-cache'

response = http.request(request)
puts response.read_body
```
> The above command returns JSON structured like this:

```json
{
  "registrations": [
      {
      "id": 123456,
      "event_code": "19ALLEVAES02",
      "event_name": "2019 All Hands Executive Summit",
      "attendee_type": "Attendee",
      "first_name": "Bugs",
      "last_name": "Bunny",
      "title": "Actor",
      "organization_name": "Warner Bros.",
      "email": "bugs@warnerbros.com",
      "status": "Approved",
      "last_modified_date_time": "2018-12-19 01:22:42",
      "event_ext_value_01": "EH1111wH_AT0Sup0DoCehWh_atsUPd0c",
      "event_ext_value_02": "Speaker",
      "event_ext_value_03": "Governing Body",
      "event_hub_link": "www.hub.com/Zfg3141_rRe_deTHhhhPicab1111Eppx",
      "event_hub_pk_pass_link": "Zfg3141_rRe_deTHhhhPicab1111Eppx",
      "event_hub_qr_code_link": "www.hubpkpass.com/Zfg3141_rRe_deTHhhhPicab1111Eppx",
      "is_attended": true
    },
    {
      "id": 789101,
      "event_code": "19ALLEVAES02",
      "event_name": "2019 All Hands Executive Summit",
      "attendee_type": "Sponsor",
      "first_name": "Daffy",
      "last_name": "Duck",
      "title": "Actor",
      "organization_name": "Warner Bros.",
      "email": "daffy@warnerbros.com",
      "status": "Sponsor Approved",
      "last_modified_date_time": "2018-12-19 01:22:42",
      "event_ext_value_01": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
      "event_ext_value_02": "Speaker",
      "event_ext_value_03": null,
      "event_hub_link": "www.hub.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
      "event_hub_pk_pass_link": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
      "event_hub_qr_code_link": "www.hubpkpass.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
      "is_attended": true
    }
  ]
}
```

To get a list of all registrations for a specific event, hit this end point:

`GET /validar/registrations/event/<EVENT_CODE>?since_datetime=<year_month_date_time>`

### Query Parameters

Parameter | Options/Format | Description
--------- | ------- | -----------
since_datetime | year_month_date_time | The system should only retrieve registration records that have been last_modified after that specified date and time. Actual expected format is: "2019-03-30 01:22:42" and expected to be in UTC w/ 24-hr time.

<aside class="success">Success Response</aside>

 A successful `GET` will return a status `200 OK` with collection of registrations.

<aside class="warning">Error Response</aside>

A failed `GET` will return a status of `422 unprocessable entity` with the following potential error messages:


* `{ "error": "Event not found." }`

* `{ "error": "No registrations found." }`

## Get a Specific Registrant

```shell
  curl "http://eventbeyondapi.emt.aws.gartner.com/validar/registrations/<REGISTRATION_ID>" -H 'Authorization: Token token="<TOKEN>"' -H 'X_API_TENANT: evantaconnect' -H 'Accept: application/json, text/javascript, /; q=0.01' -H 'X_API_EMAIL: validar.api.user@evanta.com'
```
> The above command returns JSON structured like this:

```json
{
  "registration": {
    "id": 789101,
    "event_code": "19ALLEVAES02",
    "event_name": "2019 All Hands Executive Summit",
    "attendee_type": "Attendee",
    "first_name": "Daffy",
    "last_name": "Duck",
    "title": "Actor",
    "organization_name": "Warner Bros.",
    "email": "daffy@warnerbros.com",
    "status": "Approved",
    "last_modified_date_time": "2018-12-19 01:22:42",
    "event_ext_value_01": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
    "event_ext_value_02": "Speaker",
    "event_ext_value_03": "Chair",
    "event_hub_link": "www.hub.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
    "event_hub_pk_pass_link": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
    "event_hub_qr_code_link": "www.hubpkpass.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
    "is_attended": true
  }
}
```

To fetch a single registrant, hit this end point:

`GET /validar/registrations/<REGISTRATION_ID>`

<aside class="success">Success Response</aside>

A successful `GET` will return a status `200 OK` with one registrant.

<aside class="warning">Error Response</aside>

A failed `GET` will return a status of `404 Not Found`. No additional message is given.

## Create a new registrant (**Route Disabled 5/3/19**)

```shell
  curl -X POST
  -d '{ "registration": {
          "event_code": "19ALLEVAES02",
          "attendee_type": "Attendee",
          "first_name": "Elmer",
          "last_name": "Fudd",
          "title": "Actor",
          "organization_name": "Warner Bros.",
          "email": "elmer@warnerbros.com",
          "event_hub_link": "www.hub.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
          "event_hub_qr_code_link": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
          "event_hub_pk_pass_link": "www.hubpkpass.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
          "is_attended": true,
        }
    }'

  "http://eventbeyondapi.emt.aws.gartner.com/validar/registrations/789101"
  -H 'Authorization: Token token="<TOKEN>"'
  -H 'X_API_TENANT: evantaconnect'
  -H 'Accept: application/json, text/javascript, /; q=0.01'
  -H 'X_API_EMAIL: validar.api.user@evanta.com'
```

> The above command returns JSON structured like this:

```json
{
  "registration": {
    "id": 8314101,
    "event_code": "19ALLEVAES02",
    "event_name": "2019 All Hands Executive Summit",
    "attendee_type": "Attendee",
    "first_name": "Elmer",
    "last_name": "Fudd",
    "title": "Actor",
    "organization_name": "Warner Bros.",
    "email": "elmer@warnerbros.com",
    "status": "Approved",
    "last_modified_date_time": "2018-12-19 01:22:42",
    "event_ext_value_01": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
    "event_ext_value_02": null,
    "event_ext_value_03": null,
    "event_hub_link": "www.hub.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
    "event_hub_pk_pass_link": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
    "event_hub_qr_code_link": "www.hubpkpass.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
    "is_attended": true
  }
}
```

_Note: this route was not needed for our Validar implementation so it has been disabled in the API. If it should be needed in the future we can easily re-enable it. The documentation has been left here as reference._

To create a registrant use this end point:

`POST /validar/registrations`

The `event_code` and `email` fields are required and must be unique. `first_name` and `last_name` are also required. `title` and `organization_name` are optional.

If an `attendee_type` is not included in the request "Attendee" will be assigned.

<aside class="success">Success Response</aside>

A successful `POST` will return status `201 Created`. The new registrant's `last_modified_date_time` will be set to the server's datetime.

<aside class="warning">Error Response</aside>

A failed `CREATE` will return a status of `422 unprocessable entity` with the following potential error messages:

* `{ "error": "Event not found." }`

* `{ "error": "Registration not found for event: <EVENT_CODE>." }`

* `{ "error": "Email is required." }`

* `{ "error": "First name is required." }`

* `{ "error": "Last name is required." }`

* `{ "error": "Registration already exists for event: <EVENT_CODE> and user: <EMAIL>." }`


<aside class="notice">Notice</aside>

Only the fields listed in the `-d` section of the curl will be accepted by our API. Any other values are ignored. No error is given when an unaccepted value is received.

**Email Matching:**

If a user is found in our system that matches the `email` parameter sent we will use our user to create the new registrant record. This means the values returned in the JSON for `first_name`, `last_name`, `title`, and/or `organization_name` may be different than what was sent.

**Existing registration found:**

If there is already a registration record for the `event_code` and `email` passed in a `422 Unprocessable Entity` error will be returned with the message:

* `{ "error": "Registration already exists for event: <EVENT_CODE> and user: <EMAIL>." }`

## Update an already existing registrant

```shell
curl -X PUT
-d '{
  "registration": {
    "event_hub_link": "www.hub.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
    "event_hub_pk_pass_link": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
    "event_hub_qr_code_link": "www.hubpkpass.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
    "is_attended": true
  }
}'

"http://eventbeyondapi.emt.aws.gartner.com/validar/registrations/789101"
-H 'Authorization: Token token="<TOKEN>"'
-H 'X_API_TENANT: evantaconnect'
-H 'Accept: application/json, text/javascript, /; q=0.01'
-H 'X_API_EMAIL: validar.api.user@evanta.com'
```
> The above command returns JSON structured like this:

```json
{ "message": "Registration updated" }
```

To update an already existing registrant, hit this end point:

`PUT  /validar/registrations/<REGISTRATION_ID>`

<aside class="success">Success Response</aside>

A successful `PUT` will return a status `200 OK`. The updated registrant's `last_modified_date_time` will be set to the current server date and time.

<aside class="warning">Error Response</aside>

A failed `PUT` will return a status of `422 unprocessable entity` with the following potential error messages:

* `{ "error": "Registration not found." }`

* `{ "error": "Event user not found." }`

  <aside class="notice">Notice</aside>

  Only the fields listed in the `-d` section of the curl will be accepted by our API. Any other values are ignored. No error is given when an unaccepted value is received.

  Fields not sent in the request body will remain unchanged.
