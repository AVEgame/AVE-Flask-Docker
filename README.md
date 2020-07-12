# AVE-Flask-Docker
A repo for docker builds of AVE-Flask

## Configuration

### Docker compose

Example docker-compose.yml

```
version: "3.3"
services:
  caddy:
    image: caddy:2.1.1-alpine
    ports:
      - 80:80
      - 443:443
    volumes:
      - <path/to/Caddyfile>:/etc/caddy/Caddyfile
      - <path/to/caddy/data/dir>:/data
    restart: always
  aveflask:
    image: avegame/aveflask:0.1.3-ave-1.9.7
    volumes:
      - <path/to/AVE-usergames/dir>:/home/ubuntu/AVE-usergames
      - <path/to/config.json>:/home/ubuntu/app/config.json
    restart: always
```

### Caddy

Example Caddyfile

```
avegame.co.uk {
    reverse_proxy aveflask_aveflask_1:8000
}

www.avegame.co.uk {
    reverse_proxy aveflask_aveflask_1:8000
}
```