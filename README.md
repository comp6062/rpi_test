# Raspberry Pi Stable Diffusion Installer

Interactive remote-bash installer for Automatic1111 Stable Diffusion WebUI on Raspberry Pi.

## Index

1. [Remote install](#1-remote-install)
2. [GitHub setup](#2-github-setup)
3. [Interactive installer menu](#3-interactive-installer-menu)
4. [Run after install](#4-run-after-install)
5. [First run note](#5-first-run-note)
6. [GUI launcher](#6-gui-launcher)
7. [Model downloads](#7-model-downloads)
8. [Uninstall](#8-uninstall)
9. [Included files](#9-included-files)
10. [Notes](#10-notes)

## 1. Remote install

Install directly from GitHub with `curl`:

```bash
curl -sSL https://raw.githubusercontent.com/comp6062/rpi-automatic1111/main/setup_sd.sh | bash
```

or with `wget`:

```bash
wget -qO- https://raw.githubusercontent.com/comp6062/rpi-automatic1111/main/setup_sd.sh | bash
```

This installer is self-contained for remote bash installs. The GUI banner is embedded inside `setup_sd.sh`, so the remote install does not need a separate banner download.

## 2. GitHub setup

Place `setup_sd.sh` in the root of your GitHub repository.

The installer can then be run remotely with either:

```bash
curl -sSL https://raw.githubusercontent.com/comp6062/rpi-automatic1111/main/setup_sd.sh | bash
```

or

```bash
wget -qO- https://raw.githubusercontent.com/comp6062/rpi-automatic1111/main/setup_sd.sh | bash
```

## 3. Interactive installer menu

The installer opens a menu before installing:

```text
Stable Diffusion Raspberry Pi Installer
=======================================
Use the menu below to choose install options.

  1) Download included models:  OFF
  2) Install GUI launcher:      ON
  3) Create desktop shortcut:   ON
  4) Create menu launcher:      ON
  5) Install files location:    /home/admin

  6) Start install
  q) Quit
```

Options can be toggled before install starts.

Default install location is your home folder:

```bash
~/
```

With the default location, the installer creates:

```bash
~/stable-diffusion-webui
~/stable-diffusion-env
~/run_sd.sh
```

If you choose a different install location, those files are created inside that folder instead.

## 4. Run after install

Use:

```bash
~/run_sd.sh
```

If you installed to a custom folder, run:

```bash
/path/to/install/run_sd.sh
```

The run menu includes:

1. LAN mode - first run installs needed WebUI files and allows LAN access
2. Offline mode - starts without dependency checks or installs
3. Stop running - stops the running WebUI process
4. Uninstall - removes WebUI, venv, launcher files, and shortcuts

## 5. First run note

The first time you run Stable Diffusion after install, run LAN mode once while online. This allows Automatic1111 to install needed runtime files. After the first successful LAN run, offline mode can be used without checking or installing dependencies.

## 6. GUI launcher

If GUI launcher is enabled, the installer creates:

```bash
.sd_gui_app.py
.sd_gui_runner.sh
.sd_gui_banner.png
```

These are placed in the selected install location.

If desktop shortcut is enabled, the installer creates:

```bash
~/Desktop/StableDiffusionGUI.desktop
```

If menu launcher is enabled, the installer creates:

```bash
~/.local/share/applications/sd-gui.desktop
```

The GUI includes:

- LAN Mode
- Offline Mode
- Stop Running
- Uninstall
- Open Web-UI

## 7. Model downloads

Model downloads are optional in the installer.

If enabled, the installer downloads:

- `CyberRealistic_V7.0_FP16.safetensors`
- `Realistic_Vision_V5.1-inpainting.safetensors`

If disabled, no models are downloaded during setup. You can add models later in:

```bash
stable-diffusion-webui/models/Stable-diffusion/
```

## 8. Uninstall

Run:

```bash
~/run_sd.sh
```

Then choose:

```bash
4) Uninstall
```

If installed to a custom folder, run that folder's `run_sd.sh` and choose uninstall.

The uninstaller removes:

- `stable-diffusion-webui`
- `stable-diffusion-env`
- `run_sd.sh`
- GUI helper files
- desktop shortcut
- menu launcher
- `/tmp/sd_gui.pid`

## 9. Included files

- `setup_sd.sh` - interactive self-contained remote-bash installer
- `sd_gui_banner.png` - GUI banner artwork for local reference/local extracted installs
- `README.md` - this documentation

Remote install only requires `setup_sd.sh`.

## 10. Notes

- This installer is intended for Raspberry Pi OS 64-bit.
- CPU-only PyTorch is installed.
- The WebUI is pinned to the known working Automatic1111 commit used by this setup.
- Offline mode should be used only after LAN mode has completed successfully once.
