# Getting Started with `anycable-go`

AnyCable-Go is a WebSocket server for AnyCable written in Golang.

## Installation

The easiest way to install AnyCable-Go is to [download](https://github.com/anycable/anycable-go/releases) a pre-compiled binary.

MacOS users could install it with [Homebrew](https://brew.sh/)

```sh
brew install anycable-go
```

Arch Linux users can install [anycable-go package from AUR](https://aur.archlinux.org/packages/anycable-go/).

Of course, you can install it from source too:

```sh
go get -u -f github.com/anycable/anycable-go/cmd/anycable-go
```

## Usage

Run server:

```sh
$ anycable-go --rpc_host=0.0.0.0:50051 --headers=cookie,x-api-token \
              --redis_url=redis://localhost:6379/5 --redis_channel=anycable \
              --host=0.0.0.0 --port=8080

=> INFO time context=main Starting AnyCable v0.6.0 (pid: 12902)
```

You can also provide configuration parameters through the corresponding environment variables (i.e. `ANYCABLE_RPC_HOST`, `ANYCABLE_REDIS_URL`, etc.).

For more information about available options run `anycable-go -h`.

### Configuration parameters

Here is the list of the most commonly used configuration parameters and the way you can provide them:
- through environment variable
- through CLI option.

**--host**, **--port** (`ANYCABLE_HOST`, `ANYCABLE_PORT` or `PORT`)

Server host and port (default: `"localhost"` and `8080`).

**--rpc_host** (`ANYCABLE_RPC_HOST`)

RPC service address (default: `"localhost:50051"`).

**--headers** (`ANYCABLE_HEADERS`)

List of headers to proxy to RPC (default: "`cookie`").

Redis URL for pub/sub (default: `"redis://localhost:6379/5"`).

**--redis_channel** (`ANYCABLE_REDIS_CHANNEL`)

Redis channel for broadcasting (default: `"__anycable__"`).

**--log_level** (`ANYCABLE_LOG_LEVEL`)

Logging level (default: `"info"`).

**--debug** (`ANYCABLE_DEBUG`)

Enable debug mode (more verbose logging).

## Health checks

*@since v0.6.1*

Go to `/health` (you can configure the path via `--health-path`) to see the _health_ message.
You can use this endpoint as readiness/liveness check (e.g. for load balancers).

## Instrumentation

Check this [article](go_instrumentation.md).

## Troubleshooting

First, try to run `anycable-go --debug` to enable verbose logging.

The most common problem is using different Redis channels within RPC instance and `anycable-go`. Find the following line in the logs:

```
INFO time context=pubsub Subscribed to Redis channel: __anycable__
```

and make sure, that RPC server publishes messages to the specified channel.

## TLS

To secure your `anycable-go` server provide the paths to SSL certificate and private key:

```sh
anycable-go --port=443 -ssl_cert=path/to/ssl.cert -ssl_key=path/to/ssl.key

=> INFO time context=http Starting HTTPS server at 0.0.0.0:443
```

## Docker

Official docker images available at [DockerHub](https://hub.docker.com/r/anycable/anycable-go/).

### Heroku

See [heroku-anycable-go](https://github.com/anycable/heroku-anycable-go) buildpack.
