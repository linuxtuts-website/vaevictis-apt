# VaeVictis OS - APT repository

Signed APT repository for the packages written by the VaeVictis OS author.
It is served at <https://apt.linuxtuts.online/> (GitHub Pages) and contains only the files in this repository.
Main project: <https://github.com/linuxtuts-website/vaevictis-os>

## Packages

- `vaevictis-archive-keyring` 2026.10.13 - key and settings of the VaeVictis APT repository
- `vaevictis-aurora` 1.1.1 - Aurora, the VaeVictis music player

## VaeVictis OS 1.1 and later

Nothing to do: the system already trusts this repository through the package `vaevictis-archive-keyring`, with three limits:
only packages named `vaevictis-*` may come from here (a pin makes apt ignore anything else), the index is signed with the key
below, and it **expires** if it is not re-signed, so an old index cannot be served again. `sudo apt update && sudo apt upgrade`
updates these programs. To stop trusting it: `sudo apt purge vaevictis-archive-keyring`.

## VaeVictis OS 1.0 / 1.0.1 (Debian 13, amd64)

1. Download the repository key and **check its fingerprint**:

```
sudo install -d -m 0755 /etc/apt/keyrings
sudo curl -fsSLo /etc/apt/keyrings/vaevictis.gpg https://apt.linuxtuts.online/vaevictis-archive-keyring.gpg
gpg --show-keys --with-fingerprint /etc/apt/keyrings/vaevictis.gpg
```

The fingerprint must be exactly:

```
0A41 158C 1DD6 718D 3D3F  FED0 6848 6B39 B2A9 9993
```

2. Add the repository for a moment, install its key package, then let the package take over:

```
sudo tee /etc/apt/sources.list.d/vaevictis-bootstrap.sources >/dev/null <<'EOF'
Types: deb
URIs: https://apt.linuxtuts.online
Suites: vaevictis
Components: main
Signed-By: /etc/apt/keyrings/vaevictis.gpg
EOF
sudo apt update
sudo apt install vaevictis-archive-keyring vaevictis-aurora
sudo rm /etc/apt/sources.list.d/vaevictis-bootstrap.sources /etc/apt/keyrings/vaevictis.gpg
sudo apt update
```

If you added the repository with the older instructions (file `vaevictis.sources`): when apt asks about that file while
installing `vaevictis-archive-keyring`, answer `Y`, then delete `/etc/apt/keyrings/vaevictis.gpg`.

## No warranty

The packages and this repository are provided **as is, without warranty of any kind** (GPL-3.0, sections 15 and 16). They
are designed to reduce risks; none of the protections they provide is guaranteed. Installing a package from here means
trusting its signing key and its maintainer, a single private person. Full text:
[DISCLAIMER.md](https://github.com/linuxtuts-website/vaevictis-os/blob/main/DISCLAIMER.md).

## Trust

- Every package is also published, with its SHA-256, as an immutable GitHub release of the main project.
- The index files (`Release`, `InRelease`) are signed with the key above and carry an expiry date (`Valid-Until`). A published
  package version is never changed: a fix is a new version.
- Only packages named `vaevictis-*` are published here, and VaeVictis systems accept only those from here.
- What happens if the key or an account were compromised:
  [APT-REPOSITORY.md](https://github.com/linuxtuts-website/vaevictis-os/blob/main/docs/APT-REPOSITORY.md).
