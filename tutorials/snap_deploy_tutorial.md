# Snap Deploy of Arikedb Server Tutorial

For this tutorial, we will deploy arikedb in an Ubuntu server using snap, the steps and options to make the deploy in any other linux distribution that supports Snap should not be much different.

## Installing the snap

The first step is to be sure we have snap installed in out machine, modern distributions of ubuntu comes with snap installed by default, if not, we can installing it from ubuntu official repositories:

```bash
sudo apt update
sudo apt install snapd
```

Current Arikedb released is a beta version, therefore to install it from snap-store we must include the `--beta` argument to the next command:

```bash
sudo snap install arikedb --beta
```

## Configuring the server

Now we have arikedb running in our host with its default configuration. Lets modify some things. First, lets generate a config file, for that, we can use the `arikedb` tool from command line.

Type `arikedb --help` in your terminal to see all the available options:

```bash
arikedb --help
```
Output:
```
ArikeDB Administration CLI Tool

Usage: arikedb <COMMAND>

Commands:
  create-user
  list-users
  delete-user
  change-password
  change-role
  generate-conf-file
  help                Print this message or the help of the given subcommand(s)

Options:
  -h, --help  Print help
```

The command we need is `generate-conf-file`, to see how to use it we can execute it with `--help` or `-h`:

```bash
arikedb generate-conf-file -h
```
Output:
```
Usage: arikedb generate-conf-file

Options:
  -h, --help  Print help
```

In this case the command doesn't receive any additional argument, so we just execute it ans look the path of the generated config file (it is important to run this command with root privileges):

```bash
arikedb generate-conf-file
```
Output:
```
|-> Configuration file path: /var/snap/arikedb/common/config.toml
|-> Configuration file generated.
|-> Process done.
```

Now we can open the conf file at `/var/snap/arikedb/common/config.toml`. It will look similar to this:

```toml
[general]
logger_level = "info"
data_dir = "/var/snap/arikedb/common"
log_timestamps = false
license_path = "/var/lib/arikedb/license.key"

[connection]
bind_addr = "127.0.0.1"
bind_port = 6923
tls_enabled = false
tls_cert_path = ""
tls_key_path = ""
ca_path = ""

[authentication]
auth_enabled = false
session_expiration_time = 86400000
session_after_expiration_time_margin = 300000
```

Now lets edit that file. For example, in our tutorial we want to deploy an arikedb server with exposed to all network interfaces and with authentication enabled. Also we want all debug messages from the server to be printed in the service logs and we prefer use a port different from the default one. We edit the conf file and modify these parameters getting something like this

```toml
[general]
logger_level = "debug"  # To print all debug, info, warn and error messages
data_dir = "/var/snap/arikedb/common"
log_timestamps = false
license_path = "/var/lib/arikedb/license.key"

[connection]
bind_addr = "0.0.0.0"  # To expose the server to all network interfaces
bind_port = 1234  # To listen for connections on port 1234
tls_enabled = false
tls_cert_path = ""
tls_key_path = ""
ca_path = ""

[authentication]
auth_enabled = true  # To enforce clients authentication
session_expiration_time = 86400000
session_after_expiration_time_margin = 300000
```

Now we modified the configuration file we need to restart the service, in ubuntu server we do that by executing next command with root privileges

```bash
service snap.arikedb.server restart
```

If we are watching for real time server logs using:
```bash
journalctl -u snap.arikedb.server.service -f
```

We will se something like this after restart the service

```
Jul 25 23:37:55 workstation arikedb.server[13539]:     ┌────────────────────────────────────────────────────────────┐
Jul 25 23:37:55 workstation arikedb.server[13539]:     │                                                            │
Jul 25 23:37:55 workstation arikedb.server[13539]:     │                                                            │
Jul 25 23:37:55 workstation arikedb.server[13539]:     │        _             _   _               ____    ____      │
Jul 25 23:37:55 workstation arikedb.server[13539]:     │       / \     _ __  (_) | | __   ___    |  _ \  | __ )     │
Jul 25 23:37:55 workstation arikedb.server[13539]:     │      / _ \   | '__| | | | |/ /  / _ \   | | | | |  _ \     │
Jul 25 23:37:55 workstation arikedb.server[13539]:     │     / ___ \  | |    | | |   <  |  __/   | |_| | | |_) |    │
Jul 25 23:37:55 workstation arikedb.server[13539]:     │    /_/   \_\ |_|    |_| |_|\_\  \___|   |____/  |____/     │
Jul 25 23:37:55 workstation arikedb.server[13539]:     │                                                            │
Jul 25 23:37:55 workstation arikedb.server[13539]:     │                                                            │
Jul 25 23:37:55 workstation arikedb.server[13539]:     └────────────────────────────────────────────────────────────┘
Jul 25 23:37:55 workstation arikedb.server[13539]:     
Jul 25 23:37:55 workstation arikedb.server[13539]:     
Jul 25 23:37:55 workstation arikedb.server[13539]:     
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] ==================== Starting ArikeDB Server with configuration: ====================
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] General.logger_level: "debug"
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] General.data_dir: "/var/snap/arikedb/common"
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] General.log_timestamps: false
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] General.license_path: "/var/lib/arikedb/license.key"
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Connection.bind_addr: "0.0.0.0"
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Connection.bind_port: 1234
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Connection.tls_enabled: false
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Connection.tls_cert_path: ""
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Connection.tls_key_path: ""
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Connection.ca_path: ""
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Authentication.auth_enabled: true
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Authentication.session_expiration_time: 86400000
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Authentication.session_after_expiration_time_margin: 300000
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Company: Arikedb Demo License
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] License created at: ---
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] License expires at: ---
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Max collections: 4
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Max variables: 25
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] =====================================================================================
Jul 25 23:37:55 workstation arikedb.server[13539]: [INF] Server listening on 0.0.0.0:1234
```

Here in the first set of logs we can confirm all the configuration parameters the server is using

## Creating users

Since we activated client authentication, in order to let clients connect using credentials we must generate some users in the database. To do that we will use the same `arikedb` we used before. In this case let's see which options are for users management. If we execute `arikedb -h` we can see next user management commands:

 - create-user
 - list-users
 - delete-user
 - change-password
 - change-role

Let's see the arguments for `create-user`:

```bash
arikedb create-user -h
```
Output:
```
Usage: arikedb create-user --username <USERNAME> --password <PASSWORD> --role <ROLE>

Options:
  -u, --username <USERNAME>  
  -p, --password <PASSWORD>  
  -r, --role <ROLE>          [possible values: writer, viewer]
  -h, --help                
```

So, let's create an user called **admin**, with password **admin** and role **writer**. Next command needs root privileges

```bash
arikedb create-user --username admin --password admin --role writer
```
Output:
```
|-> User configuration not found. Creating new one...
|-> New user created.
```

And let's create another user with a viewer role:

```bash
arikedb create-user --username guess --password guess --role viewer
```
Output:
```
|-> New user created.
```

Now we can list current users

```bash
arikedb list-users
```
Output:
```
--- Users ---
Username: admin
Role: Writer

Username: guess
Role: Viewer

|-> Users listed.
```

In order to remove, change password and role of any existing user just follow the documentation provided when execute the command with `-h`.

## Consuming the server

Now we are ready to start using the server to store and read out real time data.
 - [Consuming Arikedb from python](./python_client_tutorial.md)
 - [Consuming Arikedb from rust](./rust_client_tutorial.md)

[Back](../README.md)
