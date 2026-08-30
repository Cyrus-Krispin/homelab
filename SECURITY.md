# Security policy

## Scope

This repository contains sanitized documentation, diagrams, and examples. It must not contain live credentials, private keys, authentication tokens, tailnet addresses, LAN addresses, device identifiers, or unredacted service configuration.

## Reporting a problem

If sensitive information is found in the repository, do not open a public issue containing the information. Contact the repository owner privately and identify only the affected file and revision.

## Repository hygiene

- Keep raw inventory output outside version control.
- Use placeholders in configuration examples.
- Review staged changes for credentials and internal addressing before every push.
- Treat removal from the latest revision as insufficient if a secret entered Git history; rotate the secret and rewrite history where appropriate.

This policy describes repository handling. The live system's security posture is documented separately in [docs/security.md](docs/security.md).
