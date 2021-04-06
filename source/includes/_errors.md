# Errors

We use conventional HTTP response codes to indicate the success or failure of an API request. In general: Codes in the 2xx range indicate success. Codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted, invalid parameter, etc.). Codes in the 5xx range indicate an error with Bank 3's servers (these are rare).

Some 4xx errors that could be handled programmatically (e.g., parameter invalid) include an error code that briefly explains the error reported.

### HTTP Status Code Summary

#### 200, 201, 202, 204 - Successful

Everything worked as expected.

#### 400 - Bad Request

The request was unacceptable, often due to missing a required parameter, or invalid format for one.

#### 401 - Unauthorized

No valid API key provided.

#### 402 - Request Failed

The parameters were valid but the request failed.

#### 403 - Forbidden

The API key doesn't have permissions to perform the request.

#### 404 - Not Found

The requested resource doesn't exist.

#### 409 - Conflict

The request conflicts with another request (perhaps due to using the same idempotent key).

#### 429 - Too Many Requests

Too many requests hit the API too quickly. We recommend an exponential backoff of your requests.

#### 500, 502, 503, 504 - Server Errors

Something went wrong on Bank 3's end. (These are rare.)

### Attributes

#### type

The type of error returned. See below for options

#### message

A human-readable message providing more details about the error. For card errors, these messages can be shown to your users.

#### param

The parameter sent that caused the error.

### Error Types

#### authentication_error

We've received wrong credentials for this request. Usually this means you have provided work information for `client_id` and `client_secret`. Check this and try again.

#### invalid_request_error

Invalid request errors arise when your request has invalid parameters.

#### validation_error

Errors triggered when failing to validate fields (e.g., when an amount, or expiration date is invalid or incomplete).

#### api_connection_error

Failure to connect to Bank 3's API.

#### api_error

API errors cover any other type of problem (e.g., a temporary problem with Bank 3's servers), and are extremely uncommon.

# Service Status

We provide a full status page you can follow to check any updates on the status of our APIs and the overall infrastructure. Check it out [here](https://status.bank3.com.br).
