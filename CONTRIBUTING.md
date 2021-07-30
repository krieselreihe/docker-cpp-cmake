# Contributing

## Build image

To build the image run the following commands (replace `X.X.X` with the desired new version).

```shell
docker build images
docker build -t krieselreihe/docker-cpp-cmake:X.X.X images
```

## Publish image

```shell
docker push krieselreihe/docker-cpp-cmake:X.X.X
```
