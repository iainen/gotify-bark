# gotify-bark
A simple program forward gotify message to bark

## Docker Installation

Setting up gotify/server and bark server,
[gotify/server](https://github.com/gotify/server) and
[Finb/bark-server](https://github.com/Finb/bark-server)


`/app/data` contains the database file (if sqlite is used).

`gotify-bark.env` [.env.example](.env.example).

The time zone inside the container is configurable via the `TZ` environment variable: -e TZ="Europe/Berlin"

Docker RUN：

```bash
$ docker run -dt -e TZ="Europe/Berlin" --env-file /var/gotify-bark/.env --name gotify-bark -p 8080:8080 -v /var/gotify-bark/data:/app/data bnsui/gotify-bark
```

### Supported Platforms:

- amd64 (64bit)
- arm64 (ARMv8)
