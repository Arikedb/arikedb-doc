## Connection Configuration Section

Arikedb server configurations are divided in some sections. Lets break down the connection section, its parameters and all the options to set them up.

In the `config.toml` file, you can find this parameters under the section `[connection]`. A basic example configuration of this section is:
```toml
[connection]
bind_addr = "127.0.0.1"
bind_port = 6923
tls_enabled = false
tls_cert_path = ""
tls_key_path = ""
ca_path = ""
```

### Bind Addr
For Docker deployments it can also be set using the env variable `ARIKEDB_BIND_ADDR`

[Back](../README.md)
