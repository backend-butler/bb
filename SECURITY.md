# Security policy

`bb` is the boundary between an AI agent and real credentials. A bug here is treated as serious by default.

Report privately with **Security → Report a vulnerability**, never in a public issue. You should hear back within a few
days.

In scope, among others:

- A caller reaching an endpoint, host, operation or HTTP method that is not in the registry.
- A credential appearing in output, logs, the audit trail, environment or process arguments.
- Escaping the `sudoers` rule, or running as the vault user outside a broker.
- Argument injection into a shell, `ssh`, `curl` or similar.

Only the latest release gets fixes.
