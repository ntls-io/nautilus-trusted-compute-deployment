# nautilus-trusted-compute-deployment
This is a Docker Compose based deployment of [nautilus-trusted-compute](https://github.com/ntls-io/nautilus-trusted-compute).

## Services

### HTTP ingress: `nginx-proxy`

This runs [nginx-proxy] and exposes ports 80 and 443, forwarding HTTP requests through to the other services (which listen on internal ports).

[nginx-proxy]: https://github.com/nginx-proxy/nginx-proxy

#### Configuration

TLS certificates are mounted from `/etc/nginx/certs` on the host, and the proxied services use `VIRTUAL_HOST` and `CERT_NAME` to configure which host name and certificate should proxy to them.

### Vault APIs: `vault-*-api`

These run the individual Wallet TEEs using the host's SGX devices, each with a Docker volume to persist wallet state (`/app/wallet_store`).

