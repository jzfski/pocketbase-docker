# pocketbase-docker

PocketBase doesn't have an official Docker image yet, but you could use the below Dockerfile as an example:

```Dockerfile
FROM alpine:latest

ARG PB_VERSION=0.22.13

ARG ARCH=amd64

RUN apk add --no-cache \
    unzip \
    ca-certificates

# download and unzip PocketBase
ADD https://github.com/pocketbase/pocketbase/releases/download/v${PB_VERSION}/pocketbase_${PB_VERSION}_linux_${ARCH}.zip /tmp/pb.zip
RUN unzip /tmp/pb.zip -d /pb/

# uncomment to copy the local pb_migrations dir into the image
# COPY ./pb_migrations /pb/pb_migrations

# uncomment to copy the local pb_hooks dir into the image
# COPY ./pb_hooks /pb/pb_hooks

EXPOSE 8080

# start PocketBase
CMD ["/pb/pocketbase", "serve", "--http=0.0.0.0:8080"]
```
To persist your data you need to mount a volume at `/pb/pb_data`.
