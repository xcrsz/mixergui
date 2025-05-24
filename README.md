# Mixer GUI (OSS / PulseAudio)

## Description

This application provides a GTK3-based graphical user interface for managing audio settings on FreeBSD systems. It supports both the native OSS (Open Sound System) via the `mixer` command and the PulseAudio sound server via the `pactl` command, with automatic backend detection.

Users can select audio devices, view and control multiple channels simultaneously with vertical sliders, manage mute states, and filter channels. The application also supports saving and loading audio profiles.

## Target Platform

* Primarily designed for **FreeBSD** and **GhostBSD**.
* Supports **OSS** (Open Sound System) as the native backend.
* Supports **PulseAudio** as an alternative backend, which will be auto-detected if PulseAudio is active.

## Features

* **Dual Audio Backend Support:**
    * **OSS Backend:** Interacts with the system's `mixer` command.
    * **PulseAudio Backend:** Interacts with the `pactl` command-line tool.
    * Automatic detection of PulseAudio at startup; falls back to OSS if PulseAudio is not active.
* **Audio Device Selection:** Dropdown menu to select from available audio devices (OSS mixers or PulseAudio sinks/sources).
* **Multi-Channel Display:**
    * Displays multiple channels for the selected OSS device.
    * Displays a "Master" control for selected PulseAudio sinks/sources.
    * Vertical volume sliders for each displayed channel.
* **Per-Channel Controls:**
    * Individual mute/unmute checkboxes for each channel.
    * Numerical display of volume percentage below each slider.
    * Visual feedback for mute state (volume slider greys out when muted).
* **Channel Filtering:**
    * Radio buttons to filter displayed channels: "All," "Playback," or "Capture."
    * Filtering logic uses flags reported by the backend (`pbk`, `rec`, `src`) and includes heuristics for common recording channel names (e.g., "mic", "line") for the "Capture" view.
* **Profile Management:**
    * Save current audio settings (selected device, channel volumes/mutes, filter mode) to a `userProfile.json` file.
    * Load settings from the profile.
    * Settings are saved per audio device.
* **Set as System Default:**
    * For PulseAudio devices (sinks/sources), a button allows setting the selected device as the system default.
    * For OSS devices, the button provides an informational dialog with the `sysctl` command to set the default manually (requires root privileges).
* **Status and Device Information:**
    * Labels display the currently selected device, active audio backend, current filter, and status messages/errors.

## Running the Application

Execute the compiled binary from your terminal:
```bash
./mixergui
```

## Future Enhancements (Ideas)

  * Keyboard navigation for selecting devices, channels, and adjusting controls.
  * More detailed visual customization of channel strips.
  * Display and control for stereo balance if provided by the backend.
  * Option to manually select the audio backend (OSS vs. PulseAudio) if auto-detection is not desired.
  * More robust parsing and error handling for backend command outputs.
