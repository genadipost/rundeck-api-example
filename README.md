# rundeck-api-example

- #### Run job without arguments
 The following curl command will run ```job-id``` without parameters. Authentication method is with Auth-Token. The response will be in a json format (supported from API version 14).
```sh
curl -X "POST" -H "Accept: application/json" -H "Content-Type: application/json" -H "X-Rundeck-Auth-Token: <auth-token>" http://<host:port>/api/18/<job-id>/hostname/run
```

- #### List auth tokens
The following curl command will list all existing tokens. Authentication method is with Auth-Token. The response will be in a json format (supported from API version 14).
```
curl -X "GET" -H "Accept: application/json" -H "X-Rundeck-Auth-Token: <auth-token>" http://<host:port>/api/11/tokens
```
NOTE: If you will try to run the command with admin user and the defualt acl policy you will get the following error:
```
{
  "error": true,
  "apiversion": 18,
  "errorCode": "api.error.item.unauthorized",
  "message": "Not authorized for action \"admin\" for Rundeck User account"
}
```
To reslove the issue an acl policy should be added for the user. The policy cannot be added to a group because all token access is under pseudo group ```api_token_group```.
This acl policy will grant token administration permissions to admin user.

```
description: Admin user
context:
  application: 'rundeck'
for:
  resource:
    - equals:
        kind: user
      allow: [admin]
by:
  username: admin
```

- #### Create auth token
The following curl command will create new token for a specific user. Authentication method is with Auth-Token. The response will be in a json format (supported from API version 14).

```
curl -X "POST" -H "Accept: application/json" -H "X-Rundeck-Auth-Token: <auth-token>" http://<host:port>/api/18/tokens/<username>
```
NOTE: [For API v18 and earlier: by default the role api_token_group is set for the generated token, and the duration will be the maximum allowed token duration. If user is present in the URL, then the request content is ignored and can be empty.](http://rundeck.org/docs/api/#create-a-token)
