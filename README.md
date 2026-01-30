<p align="center">
  <img src="https://github.com/flatpak/flatpak/blob/main/flatpak.png?raw=true" alt="Flatpak icon"/>
</p>

Flatpak is a system for building, distributing, and running sandboxed
desktop applications on Linux.

See https://flatpak.org/ for more information.

Flatpak is available in the package repositories of most Linux distributions
and can be installed from there. See https://flatpak.org/setup/ for quick
setup instructions for many distributions.

## WSL (Ubuntu) troubleshooting

Flatpak expects a working systemd and D-Bus session. On Ubuntu under WSL2,
enable systemd, install D-Bus support, then restart the distro before rerunning
Flatpak commands.

```bash
sudo tee /etc/wsl.conf <<'EOF'
[boot]
systemd=true
EOF
sudo apt update
sudo apt install -y dbus-user-session flatpak policykit-1
```

Restart WSL from Windows PowerShell/Command Prompt and then manually reopen
your distro (e.g. launch Ubuntu from the Start menu or run `wsl`):

```powershell
wsl --shutdown
```

System-wide operations (such as `flatpak remote-add --system`) require polkit
authorization. If you see `Flatpak system operation ConfigureRemote not allowed for user`,
ensure the polkit daemon is running and your user is in the `sudo` group. On WSL,
system-level `flatpak remote-add` failures are typically due to missing polkit
authentication in the distro, so use `FLATPAK_FORCE_TEXT_AUTH=1` for a terminal
password prompt or `--user` to manage per-user remotes.

Community discussion happens in [#flatpak:matrix.org](https://matrix.to/#/#flatpak:matrix.org), on [the mailing list](https://lists.freedesktop.org/mailman/listinfo/flatpak), and on [the Flathub Discourse](https://discourse.flathub.org/).

Read documentation for Flatpak [here](https://docs.flatpak.org/en/latest/index.html).

# Contributing

Flatpak welcomes contributions from anyone! Here are some ways you can help:
* Fix [one of the issues](https://github.com/flatpak/flatpak/issues/) and submit a PR
* Update flatpak's translations and submit a PR
* Improve flatpak's documentation, hosted at http://docs.flatpak.org and developed over in [flatpak-docs](https://github.com/flatpak/flatpak-docs)
* Find a bug and [submit a detailed report](https://github.com/flatpak/flatpak/issues/new) including your OS, flatpak version, and the steps to reproduce
* Add your favorite application to [Flathub](https://flathub.org) by writing a flatpak-builder manifest and [submitting it](https://github.com/flathub/flathub/wiki/App-Submission)
* Improve the [Flatpak support](https://github.com/flatpak/flatpak/wiki/Distribution) in your favorite Linux distribution

# Hacking
See [CONTRIBUTING.md](CONTRIBUTING.md)

# Related Projects

Here are some notable projects in the Flatpak ecosystem:
* [Flatseal](https://github.com/tchx84/flatseal): An app for managing permissions of Flatpak apps without using the CLI
* [Flat-manager](https://github.com/flatpak/flat-manager): A tool for managing Flatpak repositories
