## Certs

Development certificates have been generated and placed in subdirectories under `certs/`.
Do **NOT** use these for production purposes.

### CA

```shell
openssl genpkey -algorithm RSA -out ca/key.pem

openssl req \
  -new \
  -x509 \
  -nodes \
  -days 3650 \
  -subj '/CN=deephaven-localhost-testing-ca' \
  -key ca/key.pem \
  -out ca/cert.pem
```

### Envoy

```shell
openssl genpkey -algorithm RSA -out envoy/key.pem

openssl req \
  -new \
  -key envoy/key.pem \
  -subj '/CN=localhost' \
  -out envoy/req.pem

openssl x509 \
  -req \
  -in envoy/req.pem \
  -CA ca/cert.pem \
  -CAkey ca/key.pem \
  -CAcreateserial \
  -days 3650 \
  -out envoy/cert.pem

cat envoy/cert.pem ca/cert.pem > envoy/cert.chain.pem
rm envoy/req.pem envoy/cert.pem

# This is so docker can get access. Not recommended for production usage.
chmod +r envoy/key.pem
```

### deephaven-foo

```shell
openssl genpkey -algorithm RSA -out deephaven-foo/key.pem

openssl req \
  -new \
  -key deephaven-foo/key.pem \
  -subj '/CN=deephaven-foo.localhost' \
  -out deephaven-foo/req.pem

openssl x509 \
  -req \
  -in deephaven-foo/req.pem \
  -CA ca/cert.pem \
  -CAkey ca/key.pem \
  -CAcreateserial \
  -days 3650 \
  -out deephaven-foo/cert.pem

cat deephaven-foo/cert.pem ca/cert.pem > deephaven-foo/cert.chain.pem
rm deephaven-foo/req.pem deephaven-foo/cert.pem

# This is so docker can get access. Not recommended for production usage.
chmod +r deephaven-foo/key.pem
```

### deephaven-bar

```shell
openssl genpkey -algorithm RSA -out deephaven-bar/key.pem

openssl req \
  -new \
  -key deephaven-bar/key.pem \
  -subj '/CN=deephaven-bar.localhost' \
  -out deephaven-bar/req.pem

openssl x509 \
  -req \
  -in deephaven-bar/req.pem \
  -CA ca/cert.pem \
  -CAkey ca/key.pem \
  -CAcreateserial \
  -days 3650 \
  -out deephaven-bar/cert.pem

cat deephaven-bar/cert.pem ca/cert.pem > deephaven-bar/cert.chain.pem
rm deephaven-bar/req.pem deephaven-bar/cert.pem

# This is so docker can get access. Not recommended for production usage.
chmod +r deephaven-bar/key.pem
```
