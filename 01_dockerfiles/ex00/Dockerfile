FROM alpine:latest
RUN apk update
RUN apk upgrade
RUN apk add vim
ENTRYPOINT ["vim"]

# docker build -t alpine_vim:v1 .
# docker run -it alpine_vim:v1