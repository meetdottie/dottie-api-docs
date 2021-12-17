# Meet Dottie API documentation

To be able to request Meet Dottie's API, you need to perform a few actions.
First need to set up an API user, and you need to acquire an authentication token using the API users credentials.

## Create API user

1. Set up a new user
2. Assign role to user
    * You should only assign the API user the least amount of privileges needed to reach your goal with the integration.

## Acquire authentication token

To acquire an authentication token (app token), you need to perform two sequential calls to endpoints.

1. Get id token
2. Get app token

### Get id token

POST https://titanemployeesapi.azurewebsites.net/api/auth/login

#### Request model

```json
{
    "email": "[EMAIL_ADRESS]",
    "password": "[PASSWORD]"
}
```

#### Response model

```json
{
    "token": "[ID_TOKEN]"
}
```

Store this token, and use when getting app token

### Get app token

POST https://titanemployeesapi.azurewebsites.net/api/auth/SingleSignOn/0

#### Request model

```json
{
    "idToken": "[ID_TOKEN]"
}
```

#### Response model

```json
{
    "token": "[APP_TOKEN]"
}
```

## Perform requests

All requests after acquiring app token must be sent with header ```Authorization: Bearer [APP_TOKEN]```;

Navigate through Meet Dottie, and check out what endpoints gets called. Later on we will expose a swagger file to use for generating a client.
