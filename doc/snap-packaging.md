# Snapcraft packaging (local development)

This repository includes a `snap/snapcraft.yaml` file intended for local
snap builds of Flatpak on Ubuntu 24.04. The configuration targets a strict
snap and disables the system helper, so only **per-user installations** are
supported inside the snap.

## Prerequisites

Install Snapcraft (and LXD if you want to build in a container):

```sh
sudo snap install snapcraft --classic
sudo snap install lxd
sudo lxd init --auto
```

## Build the snap

From the repository root:

```sh
cd /path/to/flatpak
snapcraft --use-lxd
```

If you prefer to build directly on the host, install the build dependencies
listed in `snap/snapcraft.yaml` and run:

```sh
sudo snapcraft --destructive-mode
```

## Install locally

```sh
sudo snap install --dangerous ./flatpak_*.snap
flatpak --version
```

## Notes and limitations

- The snap disables the system helper (`-Dsystem_helper=disabled`), so system
  installations are not available. Use `flatpak --user` when adding remotes or
  installing apps.
- Bubblewrap and xdg-dbus-proxy are staged to keep the snap self-contained.
