# csrv releases

Signed releases of **csrv**, a single Go binary that turns an Ubuntu/Debian server into a container host managed through MCP (Docker Compose + Caddy with automatic HTTPS). The source code lives in a private repository; this repository only publishes its releases.

## Install or upgrade

The same command installs csrv or, if it is already installed, upgrades it:

```bash
curl -fsSL https://github.com/efrain-salas/csrv-releases/releases/latest/download/install.sh | sudo bash -s -- \
  --email you@example.com --mcp-domain mcp.example.com
```

On an upgrade the options can be left out (csrv remembers them). On a server with csrv installed you can also run `sudo csrv upgrade`, or call the `csrv_upgrade` MCP tool.

## Verification

Every release's `checksums.txt` carries an ed25519 signature (`checksums.txt.sig`). `install.sh` and `csrv upgrade` refuse a release whose signature or checksum does not match the public key embedded in them:

```
-----BEGIN PUBLIC KEY-----
MCowBQYDK2VwAyEA7/4LNkVqVJ91ijlsQ33U7EWKkv+KuoxI3Bb7eNA0xu0=
-----END PUBLIC KEY-----
```

To verify by hand (OpenSSL 3):

```bash
openssl pkeyutl -verify -pubin -inkey pubkey.pem -rawin -in checksums.txt -sigfile checksums.txt.sig
sha256sum -c --ignore-missing checksums.txt
```
