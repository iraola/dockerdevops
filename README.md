### 1.7 Image for script

Build image using the tag flag to name it as curler.

```
docker build . -t curler
```

Run a non-detached container with:

`docker run -it curler`


### 1.8 Two-line Dockerfile

```
docker build . -t web-server`
docker run -it web-server
```
