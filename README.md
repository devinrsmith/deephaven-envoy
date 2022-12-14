# deephaven-envoy

A Deephaven reverse-proxy setup using [envoy](https://www.envoyproxy.io/).

```shell
docker compose up -d
```

Then, connect to [https://deephaven-foo.localhost](https://deephaven-foo.localhost) or [https://deephaven-bar.localhost](https://deephaven-bar.localhost) (you'll probably need to accept the self-signed certificate).

## Certs

Development certificates have been generated and placed in `certs/`. Do **NOT** use these for production purposes.

### CA

```shell
openssl genpkey -algorithm RSA -out ca.key

openssl req \
  -new \
  -x509 \
  -nodes \
  -days 3650 \
  -subj '/CN=deephaven-localhost-testing-ca' \
  -key ca.key \
  -out ca.crt
```

### Server

```shell
openssl genpkey -algorithm RSA -out server.key

openssl req \
  -new \
  -key server.key \
  -subj '/CN=localhost' \
  -out server.csr

openssl x509 \
  -req \
  -in server.csr \
  -CA ca.crt \
  -CAkey ca.key \
  -CAcreateserial \
  -days 3650 \
  -out server.crt

rm server.csr

cat server.crt ca.crt > server.chain.crt
```

## Related

* [deephaven-caddy](https://github.com/devinrsmith/deephaven-caddy)
* [deephaven-traefik](https://github.com/devinrsmith/deephaven-traefik)
