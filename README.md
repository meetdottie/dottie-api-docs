# Meet Dottie REST-API documentation

To be able to use Meet Dottie's API, you need to:
1. Create an API user in Dottie (that will be using the API)
2. Get an ID-token, using the credentials from above
3. Get an APP-token, using the ID-token from above
4. Use the API 🚀

All the endpoints are availible here: [API-documentation (Swagger)](https://api.dottie.no/api/swagger/index.html)

To authenticate, you need to perform two sequential calls to endpoints (points 2 and 3 above). 

## 1. Create API user

Goto [settings > integrations](https://app.dottie.no/settings/integrations/services) in Meet Dottie and click the "API-user" button. It's availible if your have EDIT rights to Dottie Settings.

This will show a window where you can create an API user that you wil be using the API on behalf of. The email of the user will be in the format dottie-api@yourdomain.com, and the password will be shown **once** to you. The API user will be assigned the roles `HR` and `ADMIN`. Check and modify priviliges to these roles accordingly in the [settings](https://app.dottie.no/settings/access)

If you need to invalidate the credentials or generate new you can use the same window.

## 2. Acquire ID-token


```POST https://titanemployeesapi.azurewebsites.net/api/auth/login```


#### Request model

```json
{
    "email": "my-email@domain.com",
    "password": "hunter2"
}
```

#### Response model

```json
{
    "token": "eyJhbGciOiJIUzI1NiJ9.SGVsbG8sIHdvcmxkIQ.onO9Ihudz3WkiauD ..."
}
```

This is the ID-token, it has a short lifespan and needs to be used in the next request

## 3. Exchange for APP-token

```POST https://titanemployeesapi.azurewebsites.net/api/auth/singlesignon/0```

#### Request model

```json
{
    "idToken": "{ID-TOKEN-FROM-ABOVE}"
}
```

#### Response model

```json
{
    "token": "eyJhbGciOiJSU0EtT0FFUCIsImVuYyI6IkExMjhHQ00ifQ.K52jFwAQJ ..."
}
```
What you recieve above is the APP-token, that can be used to access the API

## 4. Perform requests

All requests after acquiring APP-token must be sent with the header

```Authorization: Bearer {APP_TOKEN}```

from the example above, that would be:

```Authorization: Bearer eyJhbGciOiJSU0EtT0FFUCIsImVuYyI6IkExMjhHQ00ifQ.K52jFwAQJ ...```


All the endpoints are availible here: [API-documentation (Swagger)](https://api.dottie.no/api/swagger/index.html)

This is the same API as the Meet Dottie application uses, so if you are looking for a particular action, you can view the network requests in your browser (developer tools) and imitate what you see there, just remeber to use the token from this flow, and not the one in the browser.


### Using other credentials
If you dont wan't to use client credentials as this flow describes, and instead use your own ID prodvider - you can pass a avalid OAuth2 id_token issued from Azure AD or Google Workspace to authenticate against the enpoint in pt 3. These requirements need to be met:
- The user (e-mail) in the id_token needs to be present in the Dottie tenant
- The Dottie application needs to be approved with your ID provider. If your users use already user Azure AD or Google Workspace to login, this has been completed.
