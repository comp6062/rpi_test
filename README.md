# Raspberry Pi Stable Diffusion Installer

Interactive CLI installer for Automatic1111 Stable Diffusion WebUI on Raspberry Pi.

## Files in this bundle

- `setup_sd.sh` - interactive installer
- `sd_gui_banner.png` - GUI banner artwork used when installing from this bundle

The installer also contains an embedded banner fallback, so remote installs using `curl` or `wget` can still create the GUI banner even when the PNG is not downloaded separately.

## Install

From the bundle folder:

```bash
chmod +x setup_sd.sh
./setup_sd.sh
```

Remote install from GitHub:

```bash
curl -sSL https://raw.githubusercontent.com/comp6062/rpi-automatic1111/main/setup_sd.sh | bash
```

or:

```bash
wget -qO- https://raw.githubusercontent.com/comp6062/rpi-automatic1111/main/setup_sd.sh | bash
```

## Interactive options

The installer asks for:

1. Download included models on or off
2. Install the GUI launcher or not
3. Create a desktop shortcut or not
4. Create a menu launcher or not
5. Where to place installed files

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

## Run after install

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

## First run note

The first time you run Stable Diffusion after install, run LAN mode once while online. This allows Automatic1111 to install needed runtime files. After the first successful LAN run, offline mode can be used without checking or installing dependencies.

## GUI launcher

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

## Model downloads

Model downloads are optional in the installer.

If enabled, the installer downloads:

- `CyberRealistic_V7.0_FP16.safetensors`
- `Realistic_Vision_V5.1-inpainting.safetensors`

If disabled, no models are downloaded during setup. You can add models later in:

```bash
stable-diffusion-webui/models/Stable-diffusion/
```

## Uninstall

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

## Notes

- This installer is intended for Raspberry Pi OS 64-bit.
- CPU-only PyTorch is installed.
- The WebUI is pinned to the known working Automatic1111 commit used by this setup.
- Offline mode should be used only after LAN mode has completed successfully once.
