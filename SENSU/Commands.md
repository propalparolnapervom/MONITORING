# Commands



## API: Auth

[Use API keys to authenticate to Sensu](https://docs.sensu.io/sensu-go/latest/operations/control-access/use-apikeys/)


### Generate

Generate a new API key for the admin user
```
sensuctl api-key grant admin
```


### List


List all API keys
```
sensuctl api-key list
```


### Describe

To get information about an API key
```
sensuctl api-key info <api_key> --format json

```


### Revoke

To revoke an API key for the admin user
```
sensuctl api-key revoke <api_key> --skip-confirm
```


## API: Work

### Get

```
curl -H "Authorization: Key <api_key>" http://<server>:8080/api/core/v2/namespaces/default/checks
```



