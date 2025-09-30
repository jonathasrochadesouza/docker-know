# Docker Commands for Fullstack with Compose 🐳

## Build an Image (compose)

For all
```` bash
docker-compose build
````


```` bash
docker-compose build -d mongo
````

```` bash
docker-compose build -d app
````

```` bash
docker-compose build -d client
````

## List Images

```` bash
docker images
````

## Run a Container

For all
```` bash
docker-compose up -d
````

```` bash
docker-compose up -d mongo
````

```` bash
docker-compose up -d app
````

```` bash
docker-compose up -d client
````

## Check Running Containers

```` bash
docker ps
````

## Stop a Container

```` bash
docker stop <container_id>
````

## Remove an Image

```` bash
docker rmi <image_id>
````

## Force Stop a Container and kill image

```` bash
docker kill <container_id>
````

## Docker CLI References

https://docs.docker.com/reference/cli/docker/