# Mfxkit

Mfxkit service provides a barebones HTTP API for development of a Mainflux
service.

## Configuration

The service is configured using the environment variables presented in the
following table. Note that any unset variables will be replaced with their
default values.

| Variable              | Description                                             | Default |
|-----------------------|---------------------------------------------------------|---------|
| MF_MFXKIT_LOG_LEVEL   | Log level for mfxkit service (debug, info, warn, error) | error   |
| MF_MFXKIT_HTTP_PORT   | Mfxkit service HTTP port                                | 9021    |
| MF_MFXKIT_SERVER_CERT | Path to server certificate in pem format                |         |
| MF_MFXKIT_SERVER_KEY  | Path to server key in pem format                        |         |
| MF_JAEGER_URL         | Jaeger server URL                                       |         |
| MF_MFXKIT_SECRET      | Mfxkit service secret                                   | secret  |

## Deployment

The service itself is distributed as Docker container. The following snippet
provides a compose file template that can be used to deploy the service container
locally:

```yaml
version: "3"
services:
  mfxkit:
    image: mainflux/mfxkit:[version]
    container_name: [instance name]
    ports:
      - [host machine port]:[configured HTTP port]
    environment:
      MF_MFXKIT_LOG_LEVEL: [Kit log level]
      MF_MFXKIT_HTTP_PORT: [Service HTTP port]
      MF_MFXKIT_SERVER_CERT: [String path to server cert in pem format]
      MF_MFXKIT_SERVER_KEY: [String path to server key in pem format]
      MF_JAEGER_URL: [Jaeger server URL]      
      MF_MFXKIT_SECRET: [Mfxkit service secret]
```

To start the service outside of the container, execute the following shell script:

```bash
# download the latest version of the service
go get github.com/mainflux/mainflux

cd $GOPATH/src/github.com/mainflux/mainflux

# compile the mfxkit
make mfxkit

# copy binary to bin
make install

# set the environment variables and run the service
MF_MFXKIT_LOG_LEVEL=[Kit log level] MF_MFXKIT_HTTP_PORT=[Service HTTP port] MF_MFXKIT_SERVER_CERT: [String path to server cert in pem format] MF_MFXKIT_SERVER_KEY: [String path to server key in pem format] MF_JAEGER_URL=[Jaeger server URL] MF_MFXKIT_SECRET: [Mfxkit service secret] $GOBIN/mainflux-kit
```

## Usage

For more information about service capabilities and its usage, please check out
the [API documentation](swagger.yaml).

[doc]: http://mainflux.readthedocs.io
