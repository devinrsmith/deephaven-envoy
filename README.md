# deephaven-envoy

A Deephaven reverse-proxy setup using [envoy](https://www.envoyproxy.io/).

```shell
docker compose up -d
```

Then, connect to [https://deephaven-foo.localhost](https://deephaven-foo.localhost) or [https://deephaven-bar.localhost](https://deephaven-bar.localhost) (you'll probably need to accept the self-signed certificate).

## Certs

Development certificates have been generated and placed in [certs/](./certs/).
Do **NOT** use these for production purposes.

## Related

* [deephaven-caddy](https://github.com/devinrsmith/deephaven-caddy)
* [deephaven-traefik](https://github.com/devinrsmith/deephaven-traefik)
