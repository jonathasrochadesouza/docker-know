# Docker Commands for Frontend 🐳

## Build an Image

```` bash
docker build -t jonathasrochadesouza/frontend .
````

## List Images

```` bash
docker images
````

## Run a Container

```` bash
docker run -p 3000:3000 jonathasrochadesouza/frontend
````

To free console CLI, add flag '-d'
```` bash
docker run -d -p 3000:3000 jonathasrochadesouza/frontend
````

If error because version
```` bash
docker run -e "NODE_OPTIONS=--openssl-legacy-provider" -p 3000:3000 jonathasrochadesouza/frontend
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