# Nginx_certbot_reverse_proxy_Docker
Container cluster hosting using Nginx and Certbot.<br>
This YML allows you to expose containers to the internet using SSL certificates from Certbot (LetsEncrypt) using Nginx as reverse proxy.

## Usage
To run the cluster, ensure to execute the following commands:<br>
```
docker network create nginx-proxy
docker-compose up -d
```

## How to expose containers
For expose your containers, you have to add some stuff in you `docker-compose` file in order to `docker-gen` container creates the new virtual host for your web app.<br>

```
version: 3.7

services:
  some_service_you_want_to_expose:
    ...
    expose:
      - (put the port you want the container to use)
    environment:
      VIRTUAL_HOST: domain or subdomain to use
      LETSENCRYPT_HOST: domain or subdomain to use
      LETSENCRYPT_EMAIL: email to use
...
networks:
  default:
    external:
      name: nginx-proxy 
```

## Credits
This docker-compose was made using this [tutorial](https://blog.ssdnodes.com/blog/host-multiple-ssl-websites-docker-nginx/)
