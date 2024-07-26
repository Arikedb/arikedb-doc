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

The bind_address parameter specifies the network address that the database server will listen on for incoming connections. This address determines which network interface the server will use.

Usage:

 - **localhost (127.0.0.1)**: The server will only accept connections from the same host the server is running on. This is useful for development and testing purposes.
 - **0.0.0.0**: The server will accept connections from all available network interfaces, making it accessible from other machines on the network.
 - **Specific IP Address**: The server will bind to a specific IP address, restricting access to connections coming from that address.

### Bind Port
For Docker deployments it can also be set using the env variable `ARIKEDB_BIND_PORT`

The bind_port parameter specifies the port number on which the database server will listen for incoming connections. Ports are like doors to the machine; specifying a port allows clients to connect to the server through that specific door.

### TLS Enabled
For Docker deployments it can also be set using the env variable `ARIKEDB_TLS_ENABLED`

The tls_enabled parameter specifies whether Transport Layer Security (TLS) is enabled for the database server. Enabling TLS encrypts the communication between the server and its clients, providing a higher level of security. If enabled the server will require a certificate and key to establish secure connections.

### TLS Cert Path
For Docker deployments it can also be set using the env variable `ARIKEDB_TLS_CERT_PATH`

The tls_cert_path parameter specifies the file path to the TLS certificate used by the server. This certificate is used to authenticate the server to clients and establish a secure connection. For Snap deployments, take care of put the cert file into the accessible directory for the snap due to its confinement, potentially on `/var/snap/arikedb/common`. This parameter is only relevant if tls_enabled is set to true.

### TLS Key Path
For Docker deployments it can also be set using the env variable `ARIKEDB_TLS_KEY_PATH`

The tls_key_path parameter specifies the file path to the private key corresponding to the TLS certificate. This private key is used in the encryption process to establish secure communications. For Snap deployments, take care of put the cert file into the accessible directory for the snap due to its confinement, potentially on `/var/snap/arikedb/common`. This parameter is only relevant if tls_enabled is set to true.

### TLS CA Path
For Docker deployments it can also be set using the env variable `ARIKEDB_TLS_CA_PATH`

The ca_path parameter specifies the file path to the Certificate Authority (CA) certificate used to verify client certificates. For Snap deployments, take care of put the cert file into the accessible directory for the snap due to its confinement, potentially on `/var/snap/arikedb/common`. This parameter is only relevant if tls_enabled is set to true and if client certificate verification is needed.

[Back](../README.md)
