# X-Plane LSL Streamer Plugin

## Overview

The **X-Plane LSL Streamer Plugin** allows real-time streaming of flight data from X-Plane to **Lab Streaming Layer (LSL)**, making it easier to integrate with research applications, VR environments, neuroscience experiments, and other real-time data processing systems.

## Features

- Streams selected X-Plane datarefs in real-time via **LSL**.
- Configurable datarefs using a simple `config.txt` file.
- Low-latency data transmission for real-time applications.

## Installation

### 1. Download & Build

#### Option A: Precompiled Binary (Recommended)

1. Download the latest **precompiled release**.
2. Extract the contents into `X-Plane 11/Resources/plugins/`.

### 2. Configure Datarefs

The plugin reads flight data from **X-Plane datarefs** listed in `config.txt`. Each dataref has a flag (1 for enabled, 0 for disabled). Modify `config.txt` in `X-Plane 11/Resources/plugins/LSL_XPlane_Plugin/` to customize data streaming.

#### Example `config.txt`:

```
sim/flightmodel/position/latitude 1
sim/flightmodel/position/longitude 1
sim/flightmodel/position/elevation 1
sim/flightmodel/position/indicated_airspeed 1
```

## Usage

### 0. Recommended: Use LabRecorder for Data Collection
For recording LSL streams, we recommend using **LabRecorder**, a software tool designed to capture and log data from multiple LSL streams efficiently. You can download LabRecorder from the [LSL GitHub repository](https://github.com/labstreaminglayer/App-LabRecorder).

### 1. Start X-Plane

Launch X-Plane, and the plugin will automatically load.

### 2. Verify Plugin Activation

- Open **Plugins > Plugin Admin** in X-Plane.
- Look for **LSL\_XPlane\_Plugin** and ensure it is enabled.
- Check **X-Plane Log.txt** or use **XPLMDebugString** for debugging messages.

### 3. Connect with LSL Receiver

You can use **LabRecorder** to easily log your streamed data for later analysis. Alternatively, you can use Python with `pylsl` to receive streamed data:

You can use **Python** with `pylsl` to receive streamed data:

```python
import pylsl
stream = pylsl.resolve_stream('name', 'XPlaneData')
inlet = pylsl.StreamInlet(stream[0])
while True:
    sample, timestamp = inlet.pull_sample()
    print(f"Received: {sample} at {timestamp}")
```

## Troubleshooting

- **No data received?** Ensure the correct datarefs are enabled in `config.txt`.
- **X-Plane crashes?** Check if the plugin is built for the correct X-Plane version.

## License

This project is licensed under the **MIT License**.

## Acknowledgments

- **[ÆON lab](https://www.linkedin.com/in/nicolettafala/), Auburn University, PI: Dr. Nicoletta Fala**.
- **X-Plane SDK** for plugin development.
- **Lab Streaming Layer (LSL)** for real-time data integration.

---

🔗 GitHub: https://github.com/LuisjAlarcon/XPlane-LSL-Streamer

