## Compatibility

| Ballerina Language Version | Gmail API Version |  
| :-------------------------:|:-----------------:| 
| 0.970.0-beta15            | v1                | 

### Prerequisites

* To use Gmail endpoint, you need to provide the following:
    * Client Id
    * Client Secret
    * Access Token
    * Refresh Token
    
    *Please note that, providing ClientId, Client Secret, Refresh Token are optional if you are only providing a 
valid Access Token vise versa.*

* Go through the following steps to obtain client id, client secret, refresh token and access token for Gmail API.
    *   Go to Google APIs console to create a project and create an app for the project to connect with Gmail API.
    
    *   Configure the OAuth consent screen under Credentials and give a product name to shown to users.
    
    *   Create OAuth client ID credentials by selecting an application type and giving a name and a redirect URI. 

        *Give the redirect URI as (https://developers.google.com/oauthplayground), if you are using OAuth2 playground to 
        receive the authorization code and obtain access token and refresh token.*

    *   Visit OAuth 2.0 Playground and select the required Gmail API scopes. 
    *   Give previously obtained client id and client secret and obtain the refresh token and access token.

    
### Working with Gmail Connector.

In order to use the Gmail connector, first you need to create a Gmail endpoint by passing above mentioned parameters.

Visit `test.bal` file to find the way of creating Gmail endpoint.

#### Running gmail tests
In order to run the tests, the user will need to have a Gmail account and configure the `ballerina.conf` configuration
file with the obtained tokens.

###### ballerina.conf
```ballerina.conf
ACCESS_TOKEN="enter your access token here"
CLIENT_ID="enter your client id here"
CLIENT_SECRET="enter your client secret here"
REFRESH_TOKEN="enter your refresh token here"
```

Assign the values for the accessToken, clientId, clientSecret and refreshToken inside constructed endpoint in test.bal 
in either way following,
```ballerina
endpoint Client gmailEP {
    clientConfig:{
        auth:{
            accessToken:config:getAsString("ACCESS_TOKEN")
        }
    }
};
```

```ballerina
endpoint Client gmailEP {
    clientConfig:{
        auth:{
            accessToken:config:getAsString("ACCESS_TOKEN"),
            clientId:config:getAsString("CLIENT_ID"),
            clientSecret:config:getAsString("CLIENT_SECRET"),
            refreshToken:config:getAsString("REFRESH_TOKEN")
        }
    }
};
```

Assign values for the following variables defined at the top in test.bal file.
* recipient (Example: "recipient@gmail.com")
* sender (Example: "sender@gmail.com")
* cc (Example: "cc@gmail.com")
* attachmentPath (Example: "/home/user/hello.txt")
* attachmentContentType (Example: "text/plain")
* inlineImagePath (Example: "/home/user/Picture2.jpg")
* inlineImageName (Example: "Picture2.jpg")
* imageContentType (Example: "image/jpeg")

Run tests :

```
ballerina init
ballerina test gmail --config ballerina.conf
```
After a successful test run, you will receive two emails to the recipient inbox, one in text/plain with an attachment 
and other one in text/html with the same attachment. The two mails will be deleted from your sender's sent mail box as well.  