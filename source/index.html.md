---
title: Evanta API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - VERSION 1.0.0
  - © 2019. All rights reserved.

search: true
---

# Getting Started

Welcome to the Evanta Registration API for Validar.

The information contained here will help you get started, and the menu on the left will show you the specifics about submitting and retrieving data from our system. The information on the right will show you the curl commands and responses.

## Authentication
> To authorize, use this code:

```shell
curl 'https://api.eventbeyond.com/validar/registrations/event/<EVENT_CODE>' -H 'Authorization: Token token="<TOKEN>"' -H 'X_API_TENANT: evantaconnect' -H 'Accept: application/json, text/javascript, /; q=0.01' -H 'X_API_EMAIL: validar.api.user@evanta.com'
```

First things first, you must have permission to access to the public API, and that permission is granted through your Validar Admin Role.

Once you have successfully authenticated and can retrieve some information, you are ready to dig a little deeper. Check out the menu on the left for specifics about registrations.

<aside class="notice">
  You must replace TOKEN with your personal API key and EVENT_CODE with the event code you are after.
</aside>

# Registrations

A registration is made up of the following attributes:

Attribute | Type | Required | Notes
---:|:---:|:---:|:---
**id** | integer | ✔️ |  Your unique identifier
**event_code** | string | ✔️ |
**attendee_type** | string | | "Attendee" or "Sponsor"
**first_name** | string | |
**last_name** | string | |
**title** | string | |
**organization_name** | string | |
**email** | string | |
**status** | string | | "Approved" or "Sponsor Approved"
**last_modified_date_time** | datetime | |
**event_hub_link**  | string | |
**event_hub_pk_pass_link** | string | |
**event_hub_qr_code_link** | string | |
**event_ext_value_01** | string | | Evanta QR Code value
**event_ext_value_02** | string | | Ribbon value: "Speaker"
**event_ext_value_03** | string | | Ribbon value: "Governing Body" or "Chair"
**is_attended** | boolean | |


## Get All Registrations

```shell
  curl "http://api.eventbeyond.com/validar/registrations/
  event/<EVENT_CODE>?since_datetime='2018-12-19 01:22:42'" -H 'Authorization: Token token="TOKENTOKENTOKEN"' -H 'X_API_TENANT: evantaconnect' -H 'Accept: application/json, text/javascript, */*; q=0.01' -H 'X_API_EMAIL: validar.api.user@evanta.com'
```
> The above command returns JSON structured like this:

```json
{
  "registrations": [
      {
      "id": "123456",
      "event_code": "19ALLEVAES02",
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
      "event_ext_value_03": "Governing Body"
    },
    {
      "id": "789101",
      "event_code": "19ALLEVAES02",
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
      "event_ext_value_03": ""
    }
  ]
}
```

To get a list of all registrations for a specific event, hit this end point:

`GET /validar/registrations/event/<EVENT_CODE>?since_datetime=year_month_date_time`

### Query Parameters

Parameter | Options/Format | Description
--------- | ------- | -----------
since_datetime | year_month_date_time | The system should only retrieve registration records that have been last_modified after that specified date and time.

<aside class="success">Success Response</aside>

 A successful `GET` will return a status `200 OK` with collection of registrations.

<aside class="warning">Error Response</aside>

A failed `GET` will return a status of `422 unprocessable entity` with the following potential error messages:

 * "Event not found"
 * "No registrations found"

## Get a Specific Registrant - NOT YET BUILT

```shell
  curl "http://api.eventbeyond.com/validar/registrations/<REGISTRATION_ID>"

  -H 'Authorization: Token token="<TOKEN>"'
  -H 'X_API_TENANT: evantaconnect'
  -H 'Accept: application/json, text/javascript, /; q=0.01'
  -H 'X_API_EMAIL: validar.api.user@evanta.com'
```
> The above command returns JSON structured like this:

```json
{
  "registrations": [
    {
      "id" : "789101",
      "event_code" : "19ALLEVAES02",
      "attendee_type" : "Sponsor",
      "first_name" : "Daffy",
      "last_name" : "Duck",
      "title" : "Actor",
      "organization_name" : "Warner Bros.",
      "email" : "daffy@warnerbros.com",
      "status" : "Sponsor Approved",
      "last_modified_date_time" : "2018-12-19 01:22:42",
      "event_ext_value_01": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
      "event_ext_value_02": "Speaker",
      "event_ext_value_03": ""
    }
  ]
}
```

To fetch a single registrant, hit this end point:

`GET /validar/registrations/:id`

<aside class="success">Success Response</aside>

A successful `GET` will return a status `200 OK` with one registrant.

<aside class="warning">Error Response</aside>

A failed `GET` will return a status of `422 unprocessable entity` with the following potential error messages:

 * "Event not found"
 * "No registrations found"

## Create a new registrant

```shell
  curl -X POST
  -d '{ "registrations": [
        {
          "event_code" : "19ALLEVAES02",
          "attendee_type": "Attendee",
          "first_name" : "Elmer",
          "last_name" : "Fudd",
          "title" : "Actor",
          "organization_name" : "Warner Bros.",
          "email" : "elmer@warnerbros.com",
          "status" : "Approved",
          "event_ext_value_01": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
          "event_ext_value_02": "",
          "event_ext_value_03": "Speaker"
          "event_hub_link": "www.hub.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
          "event_hub_qr_code_link": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
          "event_hub_pk_pass_link": "www.hubpkpass.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx"
          "is_attended" : "true",
        }
      ]
    }'

  "http://api.eventbeyond.com/validar/registrations/789101"
  -H 'Authorization: Token token="TOKENTOKENTOKEN"'
  -H 'X_API_TENANT: evantaconnect'
  -H 'Accept: application/json, text/javascript, */*; q=0.01'
  -H 'X_API_EMAIL: validar.api.user@evanta.com'
```

> The above command returns JSON structured like this:

```json
{
  "registrations": [
    {
      "id" : "121314",

    }
  ]
}
```

To create a registrant hit this end point:

`POST /validar/registrations`

The event_code and email fields are required and must be unique.

<aside class="success">Success Response</aside>

A successful `POST` will return status `201 Created`

<aside class="warning">Error Response</aside>

A failed `CREATE` will return a status of `422 unprocessable entity` with the following potential error messages:

  * "event_code is not valid"
  * "event_code is required"
  * "email is required"

## Update an already existing registrant

```shell
  curl -X PUT
  -d '{ "registrations": [
      {
        "event_hub_link": "www.hub.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
        "event_hub_qr_code_link": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
        "event_hub_pk_pass_link": "www.hubpkpass.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx"
        "is_attended" : "true",
      }
    ]
  }'

  "http://api.eventbeyond.com/validar/registrations/789101"
  -H 'Authorization: Token token="TOKENTOKENTOKEN"'
  -H 'X_API_TENANT: evantaconnect'
  -H 'Accept: application/json, text/javascript, */*; q=0.01'
  -H 'X_API_EMAIL: validar.api.user@evanta.com'
```
> The above command returns JSON structured like this:

```json
{
  "registrations": [
    {
      "message" : "Registration updated",
    }
  ]
}
```

To update an already existing registrant, hit this end point:

`PUT  /validar/registrations/:id`

<aside class="success">Success Response</aside>

A successful `PUT` will return a status `200 OK`.

<aside class="warning">Error Response</aside>

A failed `PUT` will return a status of `422 unprocessable entity` with the following potential error messages:

  * "No registration found"
  * "No event user found"
