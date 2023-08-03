FROM ubuntu:20.04
RUN apt update
RUN apt install curl -y

WORKDIR /usr/src/app

COPY script.sh .

ENTRYPOINT ["./script.sh"]

