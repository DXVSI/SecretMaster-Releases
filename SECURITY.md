# Security policy

## Reporting a vulnerability

Use the repository's private GitHub Security Advisory reporting flow. Do not
open a public issue containing an exploit, secret value, backup archive, master
key, database, token, private SSH key or personally identifying information.

Include the affected version and platform, the smallest reproducible sequence,
the observed impact and whether the issue requires local-user access. Redact all
credential material. A maintainer will acknowledge a complete report before
requesting any additional sensitive evidence.

## Supported versions

During beta, only the newest published beta receives security fixes. Older beta
assets remain available for rollback and forensic comparison but are not
supported for continued use.

## Scope

The most important report classes are unintended plaintext persistence,
incorrect master-key selection, backup authentication bypass, cross-generation
restore corruption, stale remote callbacks mutating newer local state, command
argument leakage and release artifact tampering.

GitHub account compromise, malware already executing as the same OS user, and
credential rotation at PostgreSQL, SSH servers or other external providers are
outside the application's direct security boundary, but reports showing that
SecretMaster materially worsens those risks are still relevant.
