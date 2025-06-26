# X-Plane → LSL «Flight-Data» Plug-in

Light-weight X-Plane plug-in that streams user-selected **datarefs** to the  
[Lab Streaming Layer (LSL)](https://labstreaminglayer.org) in real time – ideal for VR cockpits, human-in-the-loop studies, flight-training analytics, or neuroscience setups that need synchronous flight parameters.

---

## ✈️ Tested builds & simulator compatibility

| Plug-in binary | Built with | Loads in | Simulator versions tested |
|----------------|-----------|----------|---------------------------|
| **`64/win.xpl`** | **x64**, SDK 4.1 | X-Plane ≥ 10.20 (64-bit) | **11.55r2**, **12.09r1** |
| **`win.xpl`**   | **Win32**, SDK 2.1 | X-Plane ≤ 10.19 (32-bit) | **9.70** |

Both binaries come from the **same source tree**; only the Visual Studio configuration changes.

---

## Features

* Real-time, low-latency streaming via **LSL**  
  (unique stream UID per PC – multiple simulators on the same LAN are now visible simultaneously).
* User-editable **`config.txt`** – enable or disable any dataref with a “1 / 0”.
* Cross-version: runs unmodified in X-Plane 9 → 12 on Windows
## Installation

### 1. Download

#### Option A: Precompiled Binary 

1. Download the latest version
2. Extract the contents into `X-Plane 11/Resources/plugins/`, for example.

### 2. Configure Datarefs

The plugin reads flight data from **X-Plane datarefs** listed in `config.txt`. Each dataref has a flag (1 for enabled, 0 for disabled). Modify `config.txt` in `X-Plane /Resources/plugins/LSL_XPlane_Plugin/` to customize data streaming.

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

You can use **Python** with `pylsl` to receive streamed data.

## License

This project is licensed under the **MIT License**.

## Acknowledgments

- **[ÆON lab](https://www.linkedin.com/in/nicolettafala/), Auburn University, PI: Dr. Nicoletta Fala**.
- **X-Plane SDK** for plugin development.
- **Lab Streaming Layer (LSL)** for real-time data integration.

---

