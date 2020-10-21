# Cloudflare Argo Tunnel with Keycloak

Create a Keycloak lab environment on the Internet using `docker-compose` and Cloudflare Argo Tunnel (`cloudflared`) with just a few commands.

## Run on Docker Desktop locally

1. Install Cloudflare Argo Tunnel binary `cloudflared` on your local desktop device [Download link](https://developers.cloudflare.com/argo-tunnel/downloads/)

2. Install Docker Desktop [Download link](https://www.docker.com/products/docker-desktop)

2. Obtain a Argo Tunnel certificate 

```
cloudflared tunnel login
```

3. Set the environment variables

```
export KEYCLOAK_USER=<keycloak admin username>
export KEYCLOAK_PASSWORD=<keycloak admin password>
export TUNNEL_HOSTNAME=<keycloak hostname>
```

4. Spin up the environment 
```
docker-compose up
```

5. Open the Keycloak's web admin UI at `https://$TUNNEL_HOSTNAME`

## Docker Cheatsheet
```
docker-compose up 
docker-compose down
docker-compose pause
docker-compose unpause
docker-compose logs -f
docker ps
```

## Known Issues

### Connection refused
```tunnel      | time="2020-02-26T08:54:50Z" level=error msg="unable to connect to the origin" error="Get http://keycloak:8080: dial tcp 172.21.0.2:8080: connect: connection refused"```

Explanation: `cloudflared` starts to connect to `keycloak` before `keycloak` is ready. 

Solution: Increase `TUNNEL_RETRIES`


## Reference
* [docker-compose file reference](https://docs.docker.com/compose/)

* [Keycloak Docker image](https://github.com/keycloak/keycloak-containers/blob/master/server/README.md)

* [Control startup and shutdown order in Compose](https://docs.docker.com/compose/startup-order/)