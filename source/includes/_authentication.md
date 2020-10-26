# Authentication

The public API is accessible without authentication and authorization.

But before you can use the go~mus reseller API or the go~mus cash point API you will have to register a user
account with an API key. Please talk to your contact person in order to get access.

Note that special prices and products might only be available for authenticated users. It is recommended to
authenticate against all endpoints.

<aside class="success">
Remember — a happy api user is an authenticated api user!
</aside>

## Token Authentication


> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: Bearer meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

go~mus expects the API key to be included in all reseller and cash point API requests to the server in a header
that looks like the following:

`Authorization: Bearer meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key. For testing, you can use this key in the demo instance.
</aside>

## Who am I

`GET https://demo.gomus.de/api/v4/whoami`

```shell
curl "https://demo.gomus.de/api/v4/whoami"
```

> The above command returns JSON structured like this:

```json
{
  "access": "reseller",
  "museums": [
    5
  ]
}
```

### Response

The JSON response contains info about the current authentication.

- access (string), will always be present with value [“user”, “cashpoint”, “reseller”, “customer”, “public”]
- museums (array of museum ids), if no "customer" or "public" and if user is limited to museums
