## Snap Installation and setup
[Get it from the Snap Store](https://snapcraft.io/arikedb)

Arikedb can be installed in any linux distribution supporting snap (This beta is only available for AMD architectures) using the command with root privileges:
```bash
snap install arikedb --beta
```

After install the arikedb snap, you can check the service running:
```bash
service snap.arikedb.server status
```

The output must show the active (running) status and the last lines of the server logs. You can see full server logs by using:
```bash
journalctl -u snap.arikedb.server.service -f
```

Any time you want to restart the server just type:
```bash
service snap.arikedb.server restart
```

To configure the runtime options, first you need to create a config.toml file. It can be done manually, or using the arikedb tool from terminal. The command above will create a default config file at `/var/snap/arikedb/common/config.toml`

```bash
arikedb generate-conf-file
```

We will talk more about `arikedb` command tool in next sections.

In the configuration file you will see all the adjustable parameters that defines how the server of arikedb runs. To modify any of them just edit the `config.toml` and restart the service as was showed below.

[Back](../README.md)
