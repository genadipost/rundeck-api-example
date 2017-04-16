# rundeck-api-example

#### Run job without arguments
 The following curl command will run ```job-id``` without parameters. Authentication method is with Auth-Token. The response will be in a json format (supported from API version 14).
```sh
curl -X "POST" -H "Accept: application/json" -H "Content-Type: application/json" -H "X-Rundeck-Auth-Token: <auth-token>" http://<host:port>/api/18/<job-id>/hostname/run
```
