# bb

Privilege-separated brokers for [Backend Butler](https://github.com/backend-butler/backend-butler). They let an AI agent
operate servers and services **without ever holding a credential**.

> **Status: early.** The brokers are being moved here from a private repository after a security review.

## How it works

```text
agent (low-privilege user) → bb → narrow sudoers rule → vault user → broker → registered endpoint
```

- The agent runs as an unprivileged user and can only call `bb`.
- `bb` hands each request to one broker through a single, narrow `sudoers` rule.
- Brokers run as a separate vault user that owns the credentials. Each broker offers **fixed operations**: the caller
  can't pick a URL, an HTTP method, or a command line.
- Every endpoint must be in a registry (non-secret) with its credential in the vault (secret).
- Every request is written to an audit log, without credential material.

| Broker | Reaches |
|---|---|
| `bb-connect` | SSH hosts in the registry (`bb run <alias> ...`) |
| `bb-arr` | Radarr and Sonarr HTTP APIs |
| `bb-unifi` | UniFi |
| `bb-firewalla` | Firewalla |

## Rules for changes

This repository is the security boundary, so it changes slowly and is kept small.

- A new operation is fixed and named; never "pass this through".
- No credential, token or host-specific value is ever committed. Registries and vaults live on the host.
- Every script passes ShellCheck, and every operation has a test.

## Security

Report problems privately: **Security → Report a vulnerability**. See [SECURITY.md](SECURITY.md).

## License

[MIT](LICENSE)
