# Threat model

## Protected assets

- local secret values and encrypted audit payloads;
- the vault master key stored by Secret Service or Windows Credential Manager;
- portable backup plaintext, backup password and recovery-wrapped master key;
- generated SSH private keys and passwords;
- GitHub CLI credentials and the set of confirmed remote targets;
- integrity and lineage of the live SQLite database during migration or restore.

## Trust boundaries

SecretMaster crosses four boundaries: the local SQLite file, the operating
system credential store, local helper processes such as `gh`, `secret-tool` and
`ssh-keygen`, and user-selected backup files. GitHub secret values are write-only
after submission; a successful response proves acceptance, not plaintext
equality.

## Main controls

- XChaCha20-Poly1305 authenticated encryption and Argon2id for portable backups;
- LibSodium secretbox payloads plus a verified vault metadata record locally;
- full encrypted-footprint checks before any first-use key creation;
- atomic multi-scope local writes and generation-aware GitHub completion;
- candidate validation, a persistent restore journal and rollback generation;
- owner-only local files where the operating system provides enforceable file
  permissions;
- bounded helper processes with private material excluded from command-line
  arguments and diagnostics;
- explicit dry-run and confirmation before remote writes or database restore.

## Explicit non-goals

The application is not a defense against an already compromised user session,
kernel or desktop account. It is not a hosted vault, an HSM, a PostgreSQL or SSH
provider adapter, and it cannot retrieve existing GitHub secret plaintext. Code
signing, automatic updates and hardware-backed keys are not part of the first
beta.

## Release assumptions

Users must verify `SHA256SUMS` from the same release. The first Windows beta is
unsigned and therefore has weaker publisher identity assurance. CI publishes
only after both package jobs and the release bundle job succeed; when an
environment reviewer is configured, that reviewer approves the publish job for
the same workflow run.
