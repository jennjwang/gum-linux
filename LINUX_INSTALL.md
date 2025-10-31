# Linux Installation Guide

GUM now supports Linux! This guide will help you install GUM with all the necessary dependencies for Linux.

## Prerequisites

### System Dependencies

On Linux, GUM requires X11 libraries for window management. Install them using your distribution's package manager:

**Ubuntu/Debian:**
```bash
sudo apt-get update
sudo apt-get install python3-xlib python3-tk python3-dev
```

**Fedora/RHEL:**
```bash
sudo dnf install python3-xlib python3-tkinter python3-devel
```

**Arch Linux:**
```bash
sudo pacman -S python-xlib tk
```

## Installation

### Option 1: Install with Linux-specific dependencies (Recommended)

```bash
pip install -e ".[linux]"
```

This will install GUM along with the Linux-specific dependencies (`python-xlib` and `ewmh`).

### Option 2: Install from source

```bash
git clone https://github.com/GeneralUserModels/gum.git
cd gum
pip install -e ".[linux]"
```

## Verifying Installation

To verify that GUM is installed correctly with Linux support:

```python
from gum.observers.screen import Screen, PLATFORM, HAS_XLIB

print(f"Platform: {PLATFORM}")
print(f"X11 support available: {HAS_XLIB}")
```

You should see:
```
Platform: Linux
X11 support available: True
```

## Features on Linux

All core GUM features are supported on Linux, including:

- Screen capture
- Window visibility detection
- Mouse/keyboard monitoring
- Multimodal observation processing

### Window Detection

On Linux, GUM uses EWMH (Extended Window Manager Hints) to detect visible windows. This works with most modern Linux desktop environments including:

- GNOME
- KDE Plasma
- XFCE
- i3
- Cinnamon
- MATE

**Note:** Wayland support is limited. If you're using Wayland, you may need to use XWayland for full functionality.

## Troubleshooting

### Import errors

If you see errors like `ModuleNotFoundError: No module named 'Xlib'`, make sure you installed the Linux dependencies:

```bash
pip install python-xlib ewmh
```

### Window visibility not working

1. Verify your window manager supports EWMH:
   ```bash
   xprop -root | grep _NET_SUPPORTING_WM_CHECK
   ```

2. If you're using Wayland, try switching to X11 or ensure XWayland is running.

### Permission issues

GUM needs permissions to monitor mouse/keyboard input and capture screenshots. Make sure your user has the necessary permissions.

## Differences from macOS

- On macOS, GUM uses `pyobjc-framework-Quartz` for window management
- On Linux, GUM uses `python-xlib` and `ewmh`
- Window identification: macOS uses `kCGWindowOwnerName`, Linux uses both window name and window class for matching

## Contributing

If you encounter issues with Linux support, please report them at:
https://github.com/GeneralUserModels/gum/issues
