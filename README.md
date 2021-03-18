# Stack Web PHP

## Get started

```
cp docker/local.env-dist docker/local.env
vim docker/nginx/conf.d/includes/YOUR_WEB_CONF_HERE.conf
composer start
```

## Docker

### Remapper l'utilisateur du container : THE RIGHT WAY

https://docs.docker.com/engine/security/userns-remap/

https://www.alexisjanvier.net/bind-user-on-docker-container

Dans `/etc/docker/daemon.json`
```
{
  "userns-remap": "pamorim"
}
```

### Troubleshouting

Error timeout with composer : `up --build" exceeded the timeout of 300 seconds.`

Fix with composer config:
```
composer config --global process-timeout 2000
```