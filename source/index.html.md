---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:

includes:
  - transactionStatus
  - errors

search: true

code_clipboard: true
---

# Introduction

The Bank 3 API is organized around [REST](https://www.w3.org/TR/2004/NOTE-ws-arch-20040211/#relwwwrest). Our API has predictable resource-oriented URLs, accepts form-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.

You can use the Bank 3 API in test mode, which does not affect your live data or interact with the banking networks. The client credentials you use to authenticate the request determines whether the request is live mode or test mode.

The Bank 3 API differs for every account as we release new versions and tailor functionality. These docs are customized to your version of the API and display your test key and test data, which only you can see.

# Authentication

> **POST** https://api.bank3.com.br/auth

```shell
curl -X POST https://api.bank3.com.br/auth \
  -H 'Content-Type: application/json' \
  -D '{
    "client_id": "",
    "client_secret": ""
  }'
```

> **200** Response

```json
{
  "access_token": "Your_Access_Token_Will_Show_Up_Here",
  "expires_in": 86400,
  "token_type": "Bearer"
}
```

In order to ensure that only authorized users and applications are allowed access to the API, we make use of the [OAuth 2.0 authorization framework](https://tools.ietf.org/html/rfc6749).

OAuth 2 provides several grant types for different use cases. For server-side integration, we will use the Client Credentials Grant.

With Client Credentials Grant (defined in RFC 6749, section 4.4) an application can directly request an Access Token from the Authorization Server by using its Client Credentials (a Client Id and a Client Secret).

Ask support if you can't find your credentials.

# Organization

## Retrieve an Organization

> **GET** https://api.bank3.com.br/organization

```shell
curl -X GET https://api.bank3.com.br/organization \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **200** Response

```json
{
  "id": "zkIAT5N3g69FAl6OUMnd",
  "organization": {
    "document": "00000000000000",
    "legal_name": "ACME LTDA",
    "trading_name": "ACME",
    "business_type": "LTDA",
    "founding_date": "2010-01-01",
    "address": {
      "street": "Avenida Landscape",
      "number": "100",
      "complement": "12o Andar",
      "neighborhood": "Centro",
      "postal_code": "38400000",
      "city": "São Paulo",
      "state": "SP"
    },
    "phone_number": "34984325252",
    "email": "fernando@portao3.com.br",
    "main_activity": "74.90-1-04"
  }
}
```

This will retrieve the users' organization information.

## Retrieve Balance

> **GET** https://api.bank3.com.br/organization/balance

```shell
curl -X GET https://api.bank3.com.br/organization/balance \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **200** Response

```json
{
  "balance": 100,
  "currency": 986
}
```

This will retrieve the users' organization current balance.

# Cards

## Create a Card

> **POST** https://api.bank3.com.br/cards

```shell
curl -X POST https://api.bank3.com.br/cards \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}' \
  -D '{
    "amount": "",
    "currency": "",
    "maxPercentageApproval": "",
    "minPercentageApproval": "",
    "activatesAt": "",
    "cancelsAt": "",
    "custom_fields": {
      "": ""
    },
  }'
```

> **201** Response

```json
{
  "id": "8frftfw3zZLyNqjzALTr",
  "number": "5285326537172425",
  "validation": "2022-07",
  "cvv": "345",
  "amount": 100,
  "currency": "986",
  "maxPercentageApproval": 1,
  "minPercentageApproval": 0,
  "activatesAt": "2021-07-01",
  "cancelsAt": "2021-08-10",
  "custom_fields": {
    "cost_center": "HR"
  }
}
```

This will issue a new virtual card number.

For security reasons, this will be the only response we are able to show you the virtual card number information, so please make sure you do all required treatments with this information on your side at this time.

### Parameters

#### amount **REQUIRED**

The amount for which the card should be generated, in cents.

#### currency

The currency that the card will be transacted. Use [ISO 4217](https://pt.wikipedia.org/wiki/ISO_4217) codes as reference. Defaults to 986.

#### maxPercentageApproval

The maximum authorization amount that will be available for approval. Should be a number greater than 0. Defaults to 1.

#### minPercentageApproval

The minimum authorization amount that will be available for approval. Should be a number between 0 and 1. Defaults to 0.

#### activatesAt **REQUIRED**

The date for which the card will be activated. Should be greater or equal than today.

#### cancelsAt **REQUIRED**

The date for which the card will be cancelled automatically. Should be greater than activation date.

#### custom_fields

Any custom fields you could use for future referral.

## Retrieve a Card

> **GET** https://api.bank3.com.br/cards/{id}

```shell
curl -X GET https://api.bank3.com.br/cards/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **200** Response

```json
{
  "id": "8frftfw3zZLyNqjzALTr",
  "amount": 100,
  "currency": "986",
  "maxPercentageApproval": 1,
  "minPercentageApproval": 0,
  "activatesAt": "2021-07-01",
  "cancelsAt": "2021-08-10",
  "custom_fields": {
    "cost_center": "HR"
  }
}
```

This will retrieve a virtual card parameters.

Please notice that this service will not return the virtual card information (such as number, validation and cvv). This information is only shown once, when you create a new card.

### Parameters

#### id **REQUIRED**

Card ID

## Update a Card

> **PUT** https://api.bank3.com.br/cards/{id}

```shell
curl -X PUT https://api.bank3.com.br/cards/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
  -D '{
    "amount": "",
    "currency": "",
    "maxPercentageApproval": "",
    "minPercentageApproval": "",
    "activatesAt": "",
    "cancelsAt": "",
    "custom_fields": {
      "": ""
    },
  }'
```

> **200** Response

```json
{
  "id": "8frftfw3zZLyNqjzALTr",
  "amount": 100,
  "currency": "986",
  "maxPercentageApproval": 1,
  "minPercentageApproval": 0,
  "activatesAt": "2021-07-01",
  "cancelsAt": "2021-08-10",
  "custom_fields": {
    "cost_center": "HR"
  }
}
```

Will update a virtual card parameters.

While updating a credit card information, you are able to change all the usage parameters, including amounts, dates, and custom fields.

By changing the dates or the amounts of an active card, we will move any funds or change the status for this card as required, so it automatically reflect's the new information you provided.

### Parameters

#### amount **REQUIRED**

The amount for which the card should be generated, in cents.

#### currency

The currency that the card will be transacted. Use [ISO 4217](https://pt.wikipedia.org/wiki/ISO_4217) codes as reference. Defaults to 986.

#### maxPercentageApproval

The maximum authorization amount that will be available for approval. Should be a number greater than 0. Defaults to 1.

#### minPercentageApproval

The minimum authorization amount that will be available for approval. Should be a number between 0 and 1. Defaults to 0.

#### activatesAt **REQUIRED**

The date for which the card will be activated. Should be greater or equal than today.

#### cancelsAt **REQUIRED**

The date for which the card will be cancelled automatically. Should be greater than activation date.

#### custom_fields

Any custom fields you could use for future referral.

## Delete a Card

> **DELETE** https://api.bank3.com.br/cards/{id}

```shell
curl -X DELETE https://api.bank3.com.br/cards/{id} \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
```

> **204** Response

```text
NO CONTENT
```

This will delete a virtual card and return any funds associated with it.

When deleting a card, we make sure that it is no longer available to receive transactions. If it was already active, we will move any funds associated with it to the main account.

## List all cards

> **GET** https://api.bank3.com.br/cards

```shell
curl -G https://api.bank3.com.br/cards \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
  -D 'status=""'
  -D 'startsActivationAt=""'
  -D 'endsActivationAt=""'
  -D 'page=""'
  -D 'pageSize=""'
```

> **200** Response

```json
{
  "data": [
    {
      "id":"8frftfw3zZLyNqjzALTr",
      "amount": 100,
      "currency": "986",
      "maxPercentageApproval": 1,
      "minPercentageApproval": 0,
      "activatesAt": "2021-07-01",
      "cancelsAt": "2021-08-10",
      "custom_fields": {
        "cost_center": "HR"
      }
    },
    {...},
    {...}
  ],
  "page": 1,
  "records": 20
}
```

Returns a list of cards you’ve previously issued. The cards are returned in sorted order, with the earlier activation date appearing first.

### Parameters

#### status

Filter by the status for the cards you are looking for.

#### startsActivationAt

Filter for the initial date a card is expected to be activated.

#### endsActivationAt

Filter for the end date a card is expected to be activated.

#### page

Page number you are retrieving. Defaults to 1.

#### pageSize

Number of results you want in each page. Defaults to 20.

## List attached transactions

> **GET** https://api.bank3.com.br/cards/{id}/transactions

```shell
curl -G https://api.bank3.com.br/cards/{id}/transactions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {token}'
  -D 'status=""'
  -D 'startsActivationAt=""'
  -D 'endsActivationAt=""'
  -D 'page=""'
  -D 'pageSize=""'
```

> **200** Response

```json
{
  "data": [
    {
      "id": "U0RPiQB8XcYnyEu6Kput",
      "date_time": 1598274503,
      "merchant_name": "ibis",
      "merchant_city": "São Paulo",
      "merchant_country": "Brasil",
      "mcc": "7011",
      "amount": 100,
      "currency": "986",
      "auth_code": "123456",
      "response_code": 0
    },
    {...},
    {...}
  ],
  "page": 1,
  "records": 3
}
```

Fetch a list of transactions that are associated to a card.

### Parameters

#### status

Filter by the status for the transactions you are looking for.

#### page

Page number you are retrieving. Defaults to 1.

#### pageSize

Number of results you want in each page. Defaults to 20.
