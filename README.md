# ArikeDB

Arikedb is a real-time database intended to be simple of use and fast runtime for high data availability and performance. The server is written completely in rust language, taking advantage of its robustness, efficiency and high performance. 

## Installation and basic setup

Currently, Arikedb is availability for **amd64** and **arm64** architectures. It can be deployed using docker, snap (on linux systems) and apt packages (on debian based systems).

### [Docker](https://hub.docker.com/r/arikedb/arikedb)

```bash
docker run -it --rm arikedb/arikedb
```

Also se the [docker tutorial](./tutorials/docker_deploy_tutorial.md) for more information.

### [Snap](https://snapcraft.io/arikedb)

```bash
sudo snap install arikedb
```

Also se the [snap tutorial](./tutorials/snap_deploy_tutorial.md) for more information.

### [Debian](https://arikedb.github.io/Arikedb-Debian-Repository)

```bash
curl -s --compressed "https://arikedb.github.io/Arikedb-Debian-Repository/KEY.gpg" | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/arikedb.gpg > /dev/null
```
```bash
sudo curl -s -o /etc/apt/sources.list.d/arikedb.list "https://arikedb.github.io/Arikedb-Debian-Repository/arikedb.list" && sudo sed -i "s/SYS_ARCH/$(dpkg --print-architecture)/g" /etc/apt/sources.list.d/arikedb.list
```
```bash
sudo apt update
```
```bash
sudo apt install arikedb
```

## Server configuration

The first step to start using Arikedb is configuring it. To start you can use the arikedb command line tool. Execute this in the terminal your instance of Arikedb is running on:

```bash
~$ arikedb -h
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
~$
```

We will use the `generate-conf-file` command to generate a configuration file for ArikeDB.

```bash
~$ sudo arikedb generate-conf-file
|-> Configuration file path: /var/snap/arikedb/common/config.toml
|-> Configuration file generated.
|-> Process done.
~$
```
Now, we can edit any of the configuration parameters we want to change on the file we just generated. Remember restart the server after editing the configuration file. Lets take a look at the defaul configuration file content and see what we can change.

```bash
~$ cat /var/snap/arikedb/common/config.toml
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
client_auth_optional = false

[authentication]
auth_enabled = false
session_expiration_time = 86400000
session_after_expiration_time_margin = 300000
```

**Note:** Even when configuration file has a license field, current version of ArikeDB doesn't require a license and can be used completely free.

### Configuration sections

 - [General](./configuration/general.md)
 - [Connection](./configuration/connection.md)
 - [Authentication](./configuration/authentication.md)

## Languages support

Arikedb is written in Rust and it can be consumed from any language that can communicate with a gRPC server. Currently, we have official support for python and nodejs.

 - [Consuming Arikedb from python](https://pypi.org/project/arikedb/)
 - [Consuming Arikedb from nodejs](https://www.npmjs.com/package/@arikedb/core)
 