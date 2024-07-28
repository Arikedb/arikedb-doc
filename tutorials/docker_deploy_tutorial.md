# Docker Deploy of Arikedb Server Tutorial

In order to deploy Arikedb using the docker image, we only need to pull it and running using the docker daemon and passing all configurations with environment variables. We may also need to create a volume to persist static data like users metadata.

## Settings configurations in env variables
In this tutorial we will create an `.env` file with all desired configurations, other options are available like passing variables directly in the command or setting them up in our orchestrator:

```
ARIKEDB_LOG_LEVEL=debug
ARIKEDB_DATA_DIR=/var/arikedb
ARIKEDB_LOG_TIMESTAMPS=true

ARIKEDB_BIND_ADDR=0.0.0.0
ARIKEDB_BIND_PORT=5000

ARIKEDB_AUTH_ENABLED=true
```

## Creating a volume

Now lets create a volume used to store the persistent data, users metadata for example:

```bash
docker volume create arikedb_volume
```
You can inspect the created volume with

```bash
docker volume inspect arikedb_volume
```
Output
```
[
    {
        "CreatedAt": "2024-07-27T23:01:35-04:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/arikedb_volume/_data",
        "Name": "arikedb_volume",
        "Options": null,
        "Scope": "local"
    }
    ...
]
```

## Running the container

Now we run the container using next command. We use the -d flag to run the container in the background:

```bash
docker run -d --name arikedb_container -p 5000:5000 -v arikedb_volume:/var/arikedb --env-file .env  arikedb/arikedb:latest
```

Now, let's check the server logs. we use the -f command in case we can see the new generated logs in real time:

```bash
docker logs -f arikedb_container
```
Output:
```

    ┌────────────────────────────────────────────────────────────┐
    │                                                            │
    │                                                            │
    │        _             _   _               ____    ____      │
    │       / \     _ __  (_) | | __   ___    |  _ \  | __ )     │
    │      / _ \   | '__| | | | |/ /  / _ \   | | | | |  _ \     │
    │     / ___ \  | |    | | |   <  |  __/   | |_| | | |_) |    │
    │    /_/   \_\ |_|    |_| |_|\_\  \___|   |____/  |____/     │
    │                                                            │
    │                                                            │
    └────────────────────────────────────────────────────────────┘
    
    
    
2024-07-28 03:11:07: [INF] ==================== Starting ArikeDB Server with configuration: ====================
2024-07-28 03:11:07: [INF] General.logger_level: "debug"
2024-07-28 03:11:07: [INF] General.data_dir: "/var/arikedb"
2024-07-28 03:11:07: [INF] General.log_timestamps: true
2024-07-28 03:11:07: [INF] General.license_path: "/var/lib/arikedb/license.key"
2024-07-28 03:11:07: [INF] Connection.bind_addr: "0.0.0.0"
2024-07-28 03:11:07: [INF] Connection.bind_port: 5000
2024-07-28 03:11:07: [INF] Connection.tls_enabled: false
2024-07-28 03:11:07: [INF] Connection.tls_cert_path: ""
2024-07-28 03:11:07: [INF] Connection.tls_key_path: ""
2024-07-28 03:11:07: [INF] Connection.ca_path: ""
2024-07-28 03:11:07: [INF] Authentication.auth_enabled: true
2024-07-28 03:11:07: [INF] Authentication.session_expiration_time: 86400000
2024-07-28 03:11:07: [INF] Authentication.session_after_expiration_time_margin: 300000
2024-07-28 03:11:07: [INF] Company: Arikedb Demo License
2024-07-28 03:11:07: [INF] License created at: ---
2024-07-28 03:11:07: [INF] License expires at: ---
2024-07-28 03:11:07: [INF] Max collections: 4
2024-07-28 03:11:07: [INF] Max variables: 25
2024-07-28 03:11:07: [INF] =====================================================================================
2024-07-28 03:11:07: [INF] Server listening on 0.0.0.0:5000

```

## Creating an user

Since we enabled the authentication for our server, next step to be able to use our deploy is create almost one user. In this case, the simplest way is enter the container terminal and use the arikedb tool:

Entering the container terminal:

```bash
docker exec -it arikedb_container bash
```

Once there, we can use the arikedb tool to create a user:

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

Now we are ready to start using the server to store and read real time data.
 - [Consuming Arikedb from python](./python_client_tutorial.md)
 - [Consuming Arikedb from rust](./rust_client_tutorial.md)

[Back](../README.md)
