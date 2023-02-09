# Meet Dottie REST-API documentation

Steps to use Dotties API:
1. Create an API-user in Dottie
2. Authenticate
3. Use the API 🚀

All endpoints are documented here: [API-documentation (Swagger)](https://api.dottie.no/swagger/index.html)

## 1. Create API user

Goto [settings > integrations > Dotties API](https://app.dottie.no/settings/integrations/api) in Meet Dottie and click the "Create API-user" button. It's available if your have EDIT access rights to Dottie Settings, and enables you to create one or more Dottie users that you will be using the API on behalf of

You will need to copy the API key from the window when you create the user, since it will **only be showed to you once**. The API user will by default be assigned the role `ADMIN`, and will have access rights according to the regular access management settings. You can assign roles as you wish to this user, or regenerate the API-key by clicking edit.

## 2. Authenticate

```POST https://api.dottie.no/api/auth/apikey```

#### Request model

```
{
    "clientId": "CLIENT ID FROM ABOVE",
    "apiKey": "API-KEY FROM ABOVE"
}
```

#### Response model

```
{
    "token": "eyJhbGciOiJIUzI1NiJ9.SGVsbG8sIHdvcmxkIQ.onO9Ihudz3WkiauD ..."
}
```

## 3. Perform requests

All requests after acquiring the auth-token must be sent with the header

```Authorization: Bearer TOKEN FROM ABOVE```

from the example above, that header would be:

```Authorization: Bearer eyJhbGciOiJSU0EtT0FFUCIsImVuYyI6IkExMjhHQ00ifQ.K52jFwAQJ ...```


All the endpoints are available here: [API-documentation (Swagger)](https://api.dottie.no/swagger/index.html)

This is the same API as the Meet Dottie application uses, so if you are looking for a particular action, you can view the network requests in your browser (developer tools) and imitate what you see there, just remember to use the token from this flow, and not the one in the browser.

### Using other credentials
If you don't want to use client credentials as this flow describes, and instead use your own ID provider - you can pass a valid OAuth2 id_token issued from Azure AD or Google Workspace to authenticate against the endpoint /auth/SingleSignOn. These requirements need to be met:
- The user (e-mail) in the id_token needs to be present in the Dottie tenant
- The Dottie application needs to be approved with your ID provider. If your users use already user Azure AD or Google Workspace to login, this has been completed.
- The audience-claim in the token needs to have the Dottie application ID set. Please contact us to receive the respective providers ID
