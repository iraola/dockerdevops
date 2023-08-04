## 1.7 Image for script

Build image using the tag flag to name it as curler.

```
docker build . -t curler
```

Run a non-detached container with:

```
docker run -it curler
```


## 1.8 Two-line Dockerfile

The image `devopsdockeruh/simple-web-service` uses ENTRYPOINT to declare which application is to be run, therefore it expects an argument, which in this case can only be "server" if you want to publish the output into a server. If we don't provide any argument, it will write the output into a local container file `text.log`.

```
docker build . -t web-server`
docker run -it web-server
```

## 1.9 Volumes

First we need to create the destination file, otherwise we get a weird behaviour (a text.log directory might be created on the host instead of a file)

```
touch 1.9/text.log
docker run -d -it -v "$(pwd)"/1.9/text.log:/usr/src/app/text.log devopsdockeruh/simple-web-service:ubuntu
```

## 1.10 Ports open


**Shell**:

```
docker run -p 127.0.0.1:8000:8080 devopsdockeruh/simple-web-service server
```

After this, we can access the required content typing the url `127.0.0.1:8000` in a brower (`localhost:8000` also works). Take into account that we can choose different values of the host port `8000`, but in this case we should not change the container's port, since it is apparently fixed by the application `simple-web-service` to `8080`

**Output**:

```	
message	"You connected to the following path: /"
path	"/"
```

We can apply the same to the output image of exercise 1.8 `web-server`, with the only difference that it does not need the parameter `server` when calling `docker run` (port `3333` chosen randomly):

```
docker run -p 127.0.0.1:3333:8080 web-server
```
