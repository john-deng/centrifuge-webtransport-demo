# Centrifuge WebTransport Demo

## Usage

### Install Centrifuge

To install Centrifuge in Linux

```bash
curl -sSLf https://centrifugal.dev/install.sh | sh
mv centrifugo ~/.local/bin/
```

> For more platform, please refer to https://centrifugal.dev/docs/getting-started/installation

## Generate config file

the config.json is generated by below command and customized according to the need for WebTransport

```bash
centrifugo genconfig
```

## Generate self signed certificate for testing

use [mkcert](https://github.com/FiloSottile/mkcert) to generate certificate

```bash
mkcert -install
mkcert localhost
```

## Start server

Start Centrifuge and http server

```bash

centififuge --config=config.json &

centififuge serve --port 3000 &

wait
```

## Start chrome 

Start chrome with the fingerprint of the certificate above

```bash
google-chrome --disable-web-security --user-data-dir="/tmp/chrome_dev" \
              --origin-to-force-quic-on=localhost:8000 \
              --ignore-cert-errors-spki-list=$(openssl x509 -in localhost.pem -pubkey -noout | openssl pkey -pubin -outform der | openssl dgst -sha256 -binary | openssl enc -base64)

```

