# Overview

A repository that automatically obtains `images` from `docker hub` with the help of `github actions`: it aims to solve the problem that it is difficult to obtain images from `docker hub` in China (mainland China).

Pull the `image` from packages (ghcr.io).

```shell
docker pull ghcr.io/acp-code/mongo
```
or

```shell
docker pull ghcr.io/acp-code/mongo:latest
```

## Example

<details>
  <summary>Reference</summary>
  
## Create a Docker Compose file for MongoDB

Rename the `mongo` image

```shell
docker tag ghcr.io/acp-code/mongo:latest mongo:8.0.4
```

Docker Compose is a powerful tool that simplifies the management of containerized applications by allowing you to define services, networks, and volumes in a single YAML file. Even when launching a single MongoDB container, as we did in this guide, Docker Compose provides significant advantages. It ensures consistency and reusability across different environments, simplifies the container lifecycle with easy-to-use commands, and lays the foundation for future scalability.

If you are developing multiple ApostropheCMS projects, it makes sense to place the `docker-compose.yml` file in a separate folder on the development partition. This approach also ensures that you don't later mix it up with any Docker Compose files you need for production deployments

Create a `docker-compose.yml` file in the appropriate folder and add the following code:

```yaml
version: '3.8'
services:
  mongo:
    image: mongo:8.0.4
    container_name: mongo-01
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

volumes:
  mongo-data:
```

## Run the container

Once you have created this `docker-compose.yml` file, all you have to do is create and start the container using the following command:

```shell
docker-compose up -d
```

Using this `-d` flag will run the container in detached mode in the background. If your development machine has enough resources, you can leave the container running, but you will have to restart it using this command or by clicking the play icon in the desktop GUI each time you restart your machine.

If you prefer, when you are not actively developing the Apostrophe project, you can shut down the container from the desktop GUI by clicking the stop icon or using:


```shell
docker-compose down
```
</details>

## License

MIT
