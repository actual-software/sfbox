# sfbox

`sfbox` gets you into your software factory box from your own laptop: it signs you in, creates the box and opens its terminal. You don't need gcloud, ssh or key files.

## Install

On macOS or Linux:

```sh
curl -fsSL https://github.com/actual-software/sfbox/releases/latest/download/install.sh | sh
```

The script picks the build for your computer, checks it against the release's `SHA256SUMS` and puts `sfbox` in `~/.local/bin`. If that folder isn't on your `PATH`, it prints the line that adds it. To install somewhere else, set `SFBOX_INSTALL_DIR` for the `sh` at the end of the pipe: `... | SFBOX_INSTALL_DIR=/path/to/bin sh`.

### Windows

In PowerShell:

```powershell
$d = "$env:LOCALAPPDATA\Programs\sfbox"; New-Item -ItemType Directory -Force $d | Out-Null
Invoke-WebRequest https://github.com/actual-software/sfbox/releases/latest/download/sfbox-windows-amd64.exe -OutFile "$d\sfbox.exe"
(Get-FileHash "$d\sfbox.exe").Hash.ToLower()
[Environment]::SetEnvironmentVariable("Path", [Environment]::GetEnvironmentVariable("Path", "User") + ";$d", "User")
```

The third line prints the file's checksum. It should match the `sfbox-windows-amd64.exe` line of the release's [`SHA256SUMS`](https://github.com/actual-software/sfbox/releases/latest/download/SHA256SUMS). Open a new terminal afterwards so it picks up the new `Path`.

## Use

```sh
sfbox login           # sign in with Google in your browser
sfbox create my-box   # make your box and watch it boot
sfbox ssh my-box      # open its terminal
sfbox ui              # see and manage your boxes in a browser on this computer
```

`sfbox help` lists every command, and `--explain` on any of them prints what it does as it runs.

This repository holds sfbox's releases.
