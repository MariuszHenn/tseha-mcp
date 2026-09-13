# Security Policy

Tseha holds your team's engineering standards and serves them to your AI agents,
so confidentiality and availability matter. This document summarises the measures
that protect your data. It mirrors our [Security & Trust page](https://tseha.io/security),
which is the authoritative version. For the legal detail, see our
[Privacy Policy](https://tseha.io/privacy) and
[Data Processing Agreement](https://tseha.io/dpa).

## Reporting a vulnerability

If you believe you have found a security vulnerability, please report it privately
to **hello@tseha.io** rather than opening a public issue. We will acknowledge your
report, investigate, and keep you informed of the resolution. Please give us a
reasonable opportunity to fix the issue before public disclosure, and do not access
or modify data that is not yours while testing. Our machine-readable contact is
published at <https://tseha.io/.well-known/security.txt>.

## Hosting & infrastructure

- **EU hosting** - The application and database run on infrastructure located in the European Union (Vercel and Neon).
- **Managed, hardened platforms** - We build on managed providers (Vercel for the app, Neon for Postgres, Upstash for rate limiting) and inherit their physical and network security.

## Encryption

- **In transit** - All traffic to the Service is encrypted with TLS.
- **At rest** - Organization content is encrypted at rest.
- **Integration secrets** - Third-party integration tokens (for example Figma) are encrypted with authenticated encryption (AES-256-GCM), each record using a unique initialization vector.

## Authentication & access control

- **Sign-in** - Members authenticate through Auth0, our managed identity provider.
- **Agent access** - AI agents connect over OAuth with PKCE; the issued token is scoped to your organization and role and can be revoked at any time.
- **Role-based access** - Four roles (Owner, Admin, Developer, User) govern write access in the admin panel, with access further scoped per project. The MCP server is read-only for every role.
- **Checked on every request** - Membership and role are re-verified on every MCP request, so a role change or revocation takes effect immediately - no token rotation needed.

## Tenant isolation

Each organization's data is logically isolated. Every data access is scoped to the
requesting organization, so one tenant cannot read another tenant's content. Your
source code is never sent to Tseha - the MCP server only serves the standards,
components, and tokens you publish.

## Audit logging & rate limiting

- **Audit log** - Administrative and access-token actions are recorded in an audit log.
- **Rate limiting** - MCP and API traffic is rate-limited; custom limits are available on Enterprise agreements.

## Backups & disaster recovery

- **Encrypted backups** - The database supports point-in-time recovery to any moment within the last 24 hours, and encrypted daily snapshots are retained for 14 days.
- **Recovering your data** - A full-database restore is reserved for catastrophic events that affect all customers. Recovering a single organization's data - for example after an accidental deletion - is handled through a separate, documented procedure that isolates and restores only that organization's records, so other tenants are never affected.
- **Disaster recovery plan** - We maintain a documented disaster-recovery procedure with recovery objectives, and test database restores periodically.

## Incident response

We maintain a documented security incident-response process covering detection,
containment, recovery, and notification. If a personal-data breach affects your
data, we notify affected customers without undue delay so you can meet your own
obligations, and notify the supervisory authority where required - within 72 hours,
consistent with the GDPR and our [DPA](https://tseha.io/dpa).

## Your data: export & deletion

- **Self-service deletion** - You can delete your account or, as an owner, your entire organization and all its content from the app at any time. Customer Content is deleted within 30 days of account closure (see the [Privacy Policy](https://tseha.io/privacy)).
- **Data export** - Owners can export their organization's data (as JSON and Markdown) at any time, directly from Settings - no request needed. If you would like help, email hello@tseha.io.
- **Subprocessors** - The third parties that process data on our behalf are listed in our [Privacy Policy](https://tseha.io/privacy) and [DPA](https://tseha.io/dpa).

## Acknowledgments

We thank everyone who reports issues to us responsibly. Researchers who ask to be
credited are listed here.
