# Docker proxy

Very simple nginx proxy configured to proxy to hosts based on subdomain

## Usage

Create a network for the proxy to access the container(s) to proxy to.
```
docker network create proxy
```

Create the container to proxy to.
```
docker run -d --name app-whoami --network proxy emilevauge/whoami
```

Create the proxy.
```
docker run -d --network proxy -p 80:80 platy/docker-proxy
```

Use the proxy.
```
http localhost/hello Host:app-whoami.example.com
```

## Notes

Currently the resolver for the proxy will look out to DNS if it doesn't find the hostname in the local docker network, so it could proxy to other domains.
```
http localhost/hello Host:www.google.com.example.com
```

