# SecretMaster

SecretMaster is a powerful desktop manager for GitHub Actions variables and
write-only secrets. It inventories repositories, environments and organizations,
protects locally stored secret values, generates passwords and SSH keypairs, and
replaces one value across selected scopes with an explicit GitHub push.

This repository contains the public website, release documentation and binary
downloads. It does not contain the private application source code. GitHub's
automatically generated "Source code" archives contain only this public
release-site repository.

## Downloads

- [Linux x86_64 AppImage](../../releases/latest/download/SecretMaster-x86_64.AppImage)
- [Windows x86_64 portable ZIP](../../releases/latest/download/SecretMaster-Windows-x86_64.zip)
- [SHA-256 checksums](../../releases/latest/download/SHA256SUMS)
- [Build information](../../releases/latest/download/build-info.json)
- [Release news feed](../../releases.atom)

The Windows beta is unsigned. Windows may show a reputation warning. Stable
Windows releases require Authenticode signing; do not treat an unsigned beta as
a stable package.

GitHub inventory and push operations require the separately installed GitHub CLI
(`gh`) authenticated for `github.com`. Local vault, backup and generation remain
available when `gh` is absent. On Linux, local vault operations additionally
require an available Secret Service and the `secret-tool` executable. SSH key
generation requires `ssh-keygen`; the password generator remains available when
`ssh-keygen` is not installed.

## Security boundary

- GitHub never returns existing secret plaintext. SecretMaster cannot import or
  compare an already stored GitHub secret value.
- "Generate and replace" changes the local desired value and, when explicitly
  enabled, writes it to selected GitHub scopes. It does not change a PostgreSQL
  role, install an SSH public key, or revoke an external credential.
- Secret values and secret-bearing audit fields in the live SQLite database are
  encrypted. Ordinary variables and metadata are not. Portable backups encrypt
  the complete archive.
- Portable backups are authenticated encrypted archives protected by a separate
  backup password. Do not sync or copy the live SQLite database as a backup.
- The platform credential store protects the master key at rest. It does not
  protect against malware already running as the same operating-system user.

Read the [threat model](THREAT-MODEL.md), [security policy](SECURITY.md),
[binary license](BINARY-LICENSE.txt) and
[third-party notices](THIRD_PARTY_NOTICES.md) before use.

## Verify a download

Download the package and `SHA256SUMS` into the same directory, then on Linux:

```fish
sha256sum --check SHA256SUMS --ignore-missing
```

On Windows, use the built-in PowerShell hash implementation:

```powershell
$file = "SecretMaster-Windows-x86_64.zip"
$matches = @(Get-Content .\SHA256SUMS | Where-Object { $_ -match "  $([regex]::Escape($file))$" })
if ($matches.Count -ne 1) { throw "Missing or duplicate checksum entry for $file" }
$expected = ($matches[0] -split '\s+')[0].ToLowerInvariant()
$actual = (Get-FileHash -Algorithm SHA256 -LiteralPath $file).Hash.ToLowerInvariant()
if ($actual -ne $expected) { throw "SHA-256 mismatch for $file" }
```

The public beta ships as an AppImage, portable Windows ZIP, checksums and a
static release site. Installers, auto-update, telemetry, an online account and a
hosted SecretMaster service are not included.
