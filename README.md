# gotify-bark
A simple program forward gotify message to bark

## Docker Installation

1.Setting up gotify/server and bark server,
[gotify/server](https://github.com/gotify/server) and
[Finb/bark-server](https://github.com/Finb/bark-server)

2.start the docker container:
`/app/data` contains the database file (if sqlite is used).
`.env` [.env.example](.env.example).
time zone: via the `TZ` environment variable, -e TZ="Europe/Berlin"

```bash
$ docker run -d --restart unless-stopped -e TZ="Europe/Berlin" --env-file /var/gotify-bark/.env --name gotify-bark -p 8080:8080 -v /var/gotify-bark/data:/app/data bnsui/gotify-bark
```

### Supported Platforms:

- amd64 (64bit)
- arm64 (ARMv8)
