# Docker

## Create an image

```bash
docker build --platform [linux/amd64|linux/arm64] -t NAME_OF_IMAGE .
```

## Inspect to get information about the image

```bash
docker inspect NAME_OF_IMAGE
```

## Tag to push to hub

```bash
docker tag NAME_OF_IMAGE:TAG USERNAME/NAME_OF_REPOSITORY:TAG
```

## Pull from hub

```bash
docker pull USERNAME/NAME_OF_REPOSITORY
```

## Run container in background

```bash
docker run -d -p 3200:3000 USERNAME/NAME_OF_REPOSITORY
```

## More

```bash
docker ps # See containers
docker images # See images
```
