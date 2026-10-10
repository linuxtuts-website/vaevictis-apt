# VaeVictis OS - APT repository

Signed APT repository for the packages written by the VaeVictis OS author.
It is served at <https://apt.linuxtuts.online/> (GitHub Pages) and contains only the files in this repository.
Main project: <https://github.com/linuxtuts-website/vaevictis-os>

## Packages

- `vaevictis-aurora` 1.1.0 - Aurora, the VaeVictis music player

## Use it (Debian 13 / VaeVictis OS, amd64)

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

2. Add the repository and install:

```
sudo tee /etc/apt/sources.list.d/vaevictis.sources >/dev/null <<'EOF'
Types: deb
URIs: https://apt.linuxtuts.online
Suites: vaevictis
Components: main
Signed-By: /etc/apt/keyrings/vaevictis.gpg
EOF
sudo apt update
sudo apt install vaevictis-aurora
```

## Trust

- Every package is also published, with its SHA-256, as an immutable GitHub release of the main project.
- The index files (`Release`, `InRelease`) are signed with the key above. A published package version is never changed: a fix is a new version.
- To stop trusting this repository: delete `/etc/apt/sources.list.d/vaevictis.sources` and `/etc/apt/keyrings/vaevictis.gpg`.
