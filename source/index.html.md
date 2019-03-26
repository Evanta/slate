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
  curl "http://api.eventbeyond.com/validar/registrations/event"

  -H 'Authorization: Token token="TOKENTOKENTOKEN"'
  -H 'X_API_TENANT: your-tenant-name'
  -H 'Accept: application/json, text/javascript, */*; q=0.01'
  -H 'X_API_EMAIL: your.name@yourcompany.com'
```

First things first, you must have permission to access to the public API, and that permission is granted through your Validar Admin Role.

Once you have successfully authenticated and can retrieve some information, you are ready to dig a little deeper. Check out the menu on the left for specifics about registrations.

<aside class="notice">
You must replace <code>TOKENTOKENTOKEN</code> with your personal API key.
</aside>

# Registrations

A registration is made up of the following attributes:

Attribute | Type | Required | Notes
:---|:---|:---:|:---
**registrant_id** | string | ✔️ |  Your unique identifier
**event_id** | string | ✔️ |
**attendee_type** | string
**first_name** | string
**last_name** | string
**company** | string
**title** | string
**email** | string | |
**status** | string | |
**last_modified_date_time** | string | |
**event_ext_value_01** | string | | biz_card_hash
**event_ext_value_02** | string | | ribbon_type_1
**event_ext_value_01** | string | | ribbon_type_2


## Get All Registrations

```shell
  curl "http://api.eventbeyond.com/validar/registrations/
  event/19ALLEVAES02?since_datetime=2018-12-19_01:22:42.71&status=approved"

  -H 'Authorization: Token token="TOKENTOKENTOKEN"'
  -H 'X_API_TENANT: your-tenant-name'
  -H 'Accept: application/json, text/javascript, */*; q=0.01'
  -H 'X_API_EMAIL: your.name@yourcompany.com'
```
> The above command returns JSON structured like this:

```json
{
  "registrations": [
      {
      "registrant_id" : "123456",
      "event_id" : "19ALLEVAES02",
      "attendee_type" : "Attendee",
      "first_name" : "Bugs",
      "last_name" : "Bunny",
      "company" : "Warner Bros.",
      "title" : "Actor",
      "email" : "bugs@warnerbros.com",
      "status" : "Approved",
      "last_modified_date_time" : "2018-12-19 01:22:42.71",
      "event_ext_value_01": "EH1111wH_AT0Sup0DoCehWh_atsUPd0c",
      "event_ext_value_02": "Governing Body",
      "event_ext_value_03": "Speaker"
    },
    {
      "registrant_id" : "789101",
      "event_id" : "19ALLEVAES02",
      "attendee_type" : "Sponsor",
      "first_name" : "Daffy",
      "last_name" : "Duck",
      "company" : "Warner Bros.",
      "title" : "Actor",
      "email" : "daffy@warnerbros.com",
      "status" : "Approved",
      "last_modified_date_time" : "2018-12-19 01:22:42.71",
      "event_ext_value_01": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
      "event_ext_value_02": "",
      "event_ext_value_03": "Speaker"
    }

  ]
}
```

To get a list of all registrations for a specific event, hit this end point:

`GET /validar/registrations/event/:event_id?since_datetime=year_month_date_time&status=approved|sponsor_approved`

### Query Parameters

Parameter | Options/Format | Description
--------- | ------- | -----------
since_datetime | year_month_date_time | The system should only retrieve registration records that have been last_modified after that specified date and time
status | approved/sponsor_approved | If you provide the `status` of "approved" or "sponsor_approved" the system should only retrieve registration records with that specified status.

<aside class="success">Success Response</aside>

 A successful `GET` will return a status `200 OK` with collection of registrations.

<aside class="warning">Error Response</aside>

A failed `GET` will return a status of `422 unprocessable entity` with the following potential error messages:

 * "event_id is not valid"
 * "event_id is required"
 * "No registrations found for the requested EventID"
 * "No registrations found with the requested Status"
 * "No registrations found since the specified date and time"

## Get a Specific Registrant

```shell
  curl "http://api.eventbeyond.com/validar/registrations/789101"

  -H 'Authorization: Token token="TOKENTOKENTOKEN"'
  -H 'X_API_TENANT: your-tenant-name'
  -H 'Accept: application/json, text/javascript, */*; q=0.01'
  -H 'X_API_EMAIL: your.name@yourcompany.com'
```
> The above command returns JSON structured like this:

```json
{
  "registrations": [
    {
      "registrant_id" : "789101",
      "event_id" : "19ALLEVAES02",
      "attendee_type" : "Sponsor",
      "first_name" : "Daffy",
      "last_name" : "Duck",
      "company" : "Warner Bros.",
      "title" : "Actor",
      "email" : "daffy@warnerbros.com",
      "status" : "Sponsor Approved",
      "last_modified_date_time" : "2018-12-19 01:22:42.71",
      "event_ext_value_01": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
      "event_ext_value_02": "",
      "event_ext_value_03": "Speaker"
    }
  ]
}
```

To fetch a single registrant, hit this end point:

`GET /validar/registrations/:registrant_id`

<aside class="success">Success Response</aside>

A successful `GET` will return a status `200 OK` with one registrant.

<aside class="warning">Error Response</aside>

A failed `GET` will return a status of `422 unprocessable entity` with the following potential error messages:

 * "registrant_id is not valid"
 * "registrant_id is required"

## Create a new registrant

```shell
  curl -X POST
  -d '{ "registrations": [
        {
          "event_id" : "19ALLEVAES02",
          "attendee_type" : "Attendee",
          "first_name" : "Elmer",
          "last_name" : "Fudd",
          "company" : "Warner Bros.",
          "title" : "Actor",
          "email" : "elmer@warnerbros.com",
          "status" : "Approved",
          "last_modified_date_time" : "2018-12-19 01:22:42.71"
        }
      ]
    }'

  "http://api.eventbeyond.com/validar/registrations/789101"
  -H 'Authorization: Token token="TOKENTOKENTOKEN"'
  -H 'X_API_TENANT: your-tenant-name'
  -H 'Accept: application/json, text/javascript, */*; q=0.01'
  -H 'X_API_EMAIL: your.name@yourcompany.com'
```

> The above command returns JSON structured like this:

```json
{
  "registrations": [
    {
      "registrant_id" : "121314",
    }
  ]
}
```

To create a registrant hit this end point:

`POST /validar/registrations`

The event_id and email fields are required and must be unique.

<aside class="success">Success Response</aside>

A successful `POST` will return status `201 Created`

<aside class="warning">Error Response</aside>

A failed `CREATE` will return a status of `422 unprocessable entity` with the following potential error messages:

  * "event_id is not valid"
  * "event_id is required"
  * "email is required"

## Update an already existing registrant

```shell
  curl -X PUT
  -d '{ "registrations": [
      {
        "registrant_id" : "789101",
        "attendee_type" : "Sponsor",
        "status" : "Sponsor Approved",
        "last_modified_date_time" : "2018-12-19 01:22:42.71",
        "event_hub_link": "www.hub.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
        "event_hub_qr_code_link": "Y0uUU_rrrRe_deTHhhhPicab1111Eppx",
        "event_hub_pk_pass_link": "www.hubpkpass.com/Y0uUU_rrrRe_deTHhhhPicab1111Eppx"
      }
    ]
  }'

  "http://api.eventbeyond.com/validar/registrations/789101"
  -H 'Authorization: Token token="TOKENTOKENTOKEN"'
  -H 'X_API_TENANT: your-tenant-name'
  -H 'Accept: application/json, text/javascript, */*; q=0.01'
  -H 'X_API_EMAIL: your.name@yourcompany.com'
```

To update an already existing registrant, hit this end point:

`PUT  /validar/registrations/:registrant_id`

<aside class="success">Success Response</aside>

A successful `PUT` will return a status `204 No Content`.

<aside class="warning">Error Response</aside>

A failed `PUT` will return a status of `422 unprocessable entity` with the following potential error messages:

 * "registrant_id is not valid"
 * "registrant_id is required"