## Authentication Configuration Section

Arikedb server configurations are divided in some sections. Lets break down the authentication section, its parameters and all the options to set them up.

In the `config.toml` file, you can find this parameters under the section `[authentication]`. A basic example configuration of this section is:

```toml
[authentication]
auth_enabled = false
session_expiration_time = 86400000
session_after_expiration_time_margin = 300000
```

### Auth Enabled
For Docker deployments it can also be set using the env variable `ARIKEDB_AUTH_ENABLED`

If authentication is enabled, then all clients connected to the server must be authenticated before making any request. Authentication is performed using a username/password credentials. (see [Arikedb Tools Tutorial](../tutorials/arikedb_tool_tutorial.md) to know how to manage users in the server).

### Session Expiration Time
For Docker deployments it can also be set using the env variable `ARIKEDB_SESSION_EXPIRATION_TIME`

When a client successfully authenticate with the server, it receive a token for future requests, avoiding send the user credentials on every request. This token has an expiration time (which can be configured with this parameter in milliseconds). If the token sent in a request is expired the server can respond with an expired status, or send a refresh token if the old one has not been expired for more than one specified time.

### Session After Expiration Time Margin
For Docker deployments it can also be set using the env variable `ARIKEDB_SESSION_AFTER_EXPIRATION_TIME_MARGIN`

When a client send an expired token, but the amount of time the token has been expired is less than this parameter, the server will respond the request and also will send a new token valid for the same period of the previous one, so the client will be able to use it in future requests without the need of authenticate again.

[Back](../README.md)
