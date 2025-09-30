# Docker Commands for Backend 🐳

## Build an Image

```` bash
docker build -t jonathasrochadesouza/backend .
````

## List Images

```` bash
docker images
````

## Run a Container

```` bash
docker run -p 4000:4000 jonathasrochadesouza/backend
````

To free console CLI, add flag '-d'
```` bash
docker run -d -p 4000:4000 jonathasrochadesouza/backend
````

If error because version
```` bash
docker run -e "NODE_OPTIONS=--openssl-legacy-provider" -p 4000:4000 jonathasrochadesouza/backend
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