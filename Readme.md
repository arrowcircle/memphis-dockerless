# Memphis.dev dockerless

Helps to run [memphis.dev](https://memphis.dev/) locally without docker.

## Requirements

* Go version 1.19+ (I used 1.20.3).
* Recent PostgreSQL (I used 14.7).
* `Procfile` process manager. [hivemind](https://github.com/DarthSim/hivemind), [overmind](https://github.com/DarthSim/overmind) (requires tmux) or [foreman](https://github.com/ddollar/foreman)

## Setup

1. Create PostreSQL db for memphis:

```bash
createdb memphis
```

2. Copy and edit memphis env variables config. Look at `METADATA_DB_USER`:

```bash
cp .env.template .env
```

3. Copy and edit rest gateway config:

```bash
cp conf/config.json.template conf/config.json
```

## Build memphis

```bash
cd ~/
git clone https://github.com/memphisdev/memphis.git
cd memphis
CGO_ENABLED=0 go build -ldflags="-w" -a -o .
cp memphis ~/memphis-dockerless/nats-server
```

## Build rest-gateway

```bash
cd ~/
git clone https://github.com/memphisdev/memphis-rest-gateway.git
cd memphis-rest-gateway
CGO_ENABLED=0 go build -ldflags="-w" -a -o .
cp rest-gateway ~/memphis-dockerless/rest-gateway
```

## Run everything

```bash
overmind start
```
