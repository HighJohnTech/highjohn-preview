# Security Policy

## Repository status

This repository is a High John Technology preview/staging repository. It should not contain production secrets, private client data, credentials, or production-only configuration.

## Reporting

Do not publish exploitable details or sensitive data in a public issue. If GitHub private vulnerability reporting is enabled, use it. Otherwise contact High John Technology through the approved business contact published on `highjohn.tech` and request a private channel before sharing sensitive details.

## Baseline rules

- Never commit real API keys, tokens, passwords, private keys, recovery codes, or customer/client data.
- Keep GitHub Actions on supported versions and use least-privilege permissions.
- Do not execute untrusted fork code in a privileged workflow context.
- Review security findings before copying preview changes into production.
- Treat this repository as staging, not as the source for production secrets or private operating data.

If a secret is committed, revoke/rotate it first, then remove it from active code and assess Git history/log exposure.