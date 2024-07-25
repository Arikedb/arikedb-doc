## Docker setup
[Get it from the Docker Hub](https://hub.docker.com/r/arikedb/arikedb)

Arikedb docker image can be pulled and ran from docker hub:
```bash
docker pull arikedb/arikedb
```

The command above will pull the image from docker hub to your local host.

Now, you can run an arikedb container with basic configurations just executing:
```bash
docker run arikedb/arikedb
```

That will run the container with the arikedb server. In this variant, configurations of the server can be set either setting the predefined environment variables or using the `conf.toml` file inside the container. We will talk more about `arikedb` command tool in next sections.

[Back](../README.md)
