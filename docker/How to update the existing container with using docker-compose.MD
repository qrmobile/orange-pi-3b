# How to update the existing container with using docker-compose.yml

1. go to the folder where have docker-compose.yml

2. type the following commands

```
docker-compose pull
docker-compose up --force-recreate --build -d
docker image prune -f
```
