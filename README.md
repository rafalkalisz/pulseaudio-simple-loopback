# pulseaudio-simple-loopback
[![PyPI Version](https://img.shields.io/pypi/v/pulseaudio-simple-loopback.svg)](https://pypi.org/project/pulseaudio-simple-loopback/)

A simple Python CLI tool for quickly setting up and tearing down PulseAudio loopback modules — ideal for routing audio between input and output devices like USB interfaces, Bluetooth headsets, and virtual sinks.

Developed because I coudn't be bothered to set it up manually every time I wanted to play on my Korg synthesizer ʅ ( ․ ⤙ ․) ʃ.

It provides two terminal commands:

- `loopback-setup`: Interactively sets up PulseAudio loopback between a selected input and output.
- `loopback-stop`: Unloads all loaded loopback modules.

---

## Installation

### Option 1: Install from PyPI (Recommended)

```bash
pip install pulseaudio-simple-loopback
```
Installs the loopback-setup and loopback-stop commands system-wide.

### Option 2: Install from source
```bash
git clone https://github.com/YOUR_USERNAME/pulseaudio-simple-loopback.git
cd pulseaudio-simple-loopback
pip install .
```

---

## Usage Example
### loopback-setup

This command walks you through selecting a source and sink from your available PulseAudio devices, and then creates a loopback between them.
```
❯ loopback-setup
                                 Available Sources                                  
┏━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Index ┃ Name                                                                     ┃
┡━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│     0 │ alsa_input.usb-Burr-Brown_from_TI_USB_Audio_CODEC-00.analog-stereo-input │
│     1 │ bluez_input.14:3F:A6:F2:83:9D                                            │
└───────┴──────────────────────────────────────────────────────────────────────────┘
Select audio source index: 0
                                   Available Sinks                                    
┏━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Index ┃ Name                                                                       ┃
┡━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│     0 │ alsa_output.usb-Burr-Brown_from_TI_USB_Audio_CODEC-00.analog-stereo-output │
│     1 │ bluez_output.14_3F_A6_F2_83_9D.1                                           │
└───────┴────────────────────────────────────────────────────────────────────────────┘
Select audio sink index: 1

Setting loopback from: alsa_input.usb-Burr-Brown_from_TI_USB_Audio_CODEC-00.analog-stereo-input to bluez_output.14_3F_A6_F2_83_9D.1
Loopback module ID: 536870918
Loopback enabled successfully
```

In some cases with Bluetooth output devices (for ex. Sony WH-1000XM4), PulseAudio may not activate the loopback immediately.

Hence, when a Bluetooth sink is selected, the script offers to quickly disconnect and reconnect the device — which usually helps:

```
Detected Bluetooth sink: bluez_output.14_3F_A6_F2_83_9D.1, MAC: 14:3F:A6:F2:83:9D
The script detected you've selected a Bluetooth device as the loopback sink.
In some instances, the device needs to be disconnected and reconnected if the loopback doesn't start properly.
Do you want to disconnect and reconnect your Bluetooth device now? [y/n]:
```
### loopback-stop

This command unloads all detected loopback modules:
```
❯ loopback-stop
Unloading module-loopback ID 536870918...
Unloaded 1 loopback module(s)
```

---

## License
MIT License. See LICENSE for details.
