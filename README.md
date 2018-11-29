# WatchTower ECR
A docker image based on [v2tec/watchtower](https://github.com/v2tec/watchtower) for use with AWS ECR.

[![Docker Pulls](https://img.shields.io/docker/pulls/rabaco/watchtower-ecr.svg?style=flat-square)](https://hub.docker.com/r/rabaco/watchtower-ecr/)
[![Docker Stars](https://img.shields.io/docker/stars/rabaco/watchtower-ecr.svg?style=flat-square)](https://hub.docker.com/r/rabaco/watchtower-ecr/)

## Usage
Run the container with the following command:
```bash
docker run -d \
  --name watchtower \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /path/to/docker-config.json:/config.json \
  -e "AWS_ACCESS_KEY_ID=<ACCESS_KEY_ID>" \
  -e "AWS_SECRET_ACCESS_KEY=<SECRET_ACCESS_KEY>" \
  rabaco/watchtower-ecr:latest --interval 45 --cleanup
```

If you prefer, you can use the docker-compose.yml
```bash
version: '3.2'
services:
  my-service:
    image: <id>.dkr.ecr.<region>.amazonaws.com/my-image:latest
  watchtower:
    image: rabaco/watchtower-ecr:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /path/to/docker-config.json:/config.json
    environment:
      AWS_ACCESS_KEY_ID: <ACCESS_KEY_ID>
      AWS_SECRET_ACCESS_KEY: <SECRET_ACCESS_KEY>
    command: --interval 45 --cleanup
```