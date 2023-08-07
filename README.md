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


## 1.11 Spring

We select `FROM openjdk:8`

**Shell:**

```
docker build . -t simple-button
docker run -p 127.0.0.1:8080:8080
```

Browsing the url `127.0.0.1:8080` we see a button that, when pressed, it shows the message "Success".


## 1.12 Frontend

Important here to use node:16 instead of a newer version

**Dockerfile:**

```Dockerfile
FROM node:16

WORKDIR /usr/src/app

COPY . .
 
# Expose port
EXPOSE 5000

# Build project
RUN npm install
RUN npm run build
RUN npm install -g serve

# Run frontend
CMD ["serve", "-s", "-l", "5000", "build"]
```

**Shell:**

```shell
docker build . -t frontend && docker run -p 127.0.0.1:5000:5000 frontend
```

**Output:**

```
Congratulations! You configured your ports correctly!
```


## 1.13 Backend

**Dockerfile:**

```Dockerfile
FROM golang:1.16

WORKDIR /usr/src/app

COPY . .

RUN go build
RUN go test ./...

EXPOSE 8080

ENV REQUEST_ORIGIN=http://localhost:5000

CMD ["./server"]
```

**Shell:**

```shell
docker build . -t backend && docker run -p 127.0.0.1:8080:8080 backend
```


## 1.14 Environment

We only need to add the adequate environment variables to point to the right addresses. In the frontend Dockerfile add:

```Dockerfile
# Set environment variable
ENV REACT_APP_BACKEND_URL=http://localhost:8080/
```

In the backend Dockerfile add:

```Dockerfile
ENV REQUEST_ORIGIN=http://localhost:5000
```

It is important to add the `http://` prior to the localhost addreses.

Then access the frontend address `localhost:5000` through a browser and press the button to verify.
