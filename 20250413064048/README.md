# Coolify basic auth

Setting basic auth on Coolify requires editing the traefik labels.

I've only needed to do it in docker compose files. Heres my snippet:


```
    labels:
      - 'traefik.http.middlewares.$UNIQUE_TO_PROJECT.basicauth.users=$USERNAME:$PASSWORD_GENERATED_BY_HTPASSWD'
```

Link to [docs](https://coolify.io/docs/knowledge-base/proxy/traefik/basic-auth#docker-compose-and-services)

Tags:

    #coolify #traefik
