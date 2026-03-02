# X-Plane LSL Gateway: Real-Time Flight Data Synchronization

**Authors**: Luis Jose Alarcon-Aneiva & Nicoletta Fala (Auburn University, AEON Lab)  
**Contact**: [lja0024@auburn.edu](mailto:lja0024@auburn.edu) · [https://aeonresearch.org/](https://aeonresearch.org/)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![X-Plane SDK](https://img.shields.io/badge/X--Plane-SDK%204.1-blue)](https://developer.x-plane.com/sdk/)

This X-Plane plugin provides a high-performance bridge between the **X-Plane Flight Simulator** and the **Lab Streaming Layer (LSL)** ecosystem. It is specifically designed for researchers in human factors, neuroergonomics, and aviation psychology who require millisecond-accurate synchronization between flight telemetry and physiological data (e.g., EEG, Eye-tracking, ECG).

---

## 🔬 Academic Citations

If this plugin facilitates your research, please cite our work:

> Alarcon-Aneiva, L. J., & Fala, N. (2025). **Real-Time Synchronization of Flight Simulation and Physiological Data Using Lab Streaming Layer: A Custom X-Plane Approach.** *Proceedings of the 23rd International Symposium on Aviation Psychology*, 23, 222–227. [[Full Paper PDF](https://corescholar.libraries.wright.edu/isap_2025/38/)]

### BibTeX
```bibtex
@inproceedings{alarcon-aneiva2025-realtime-lsl-xplane,
  author    = {Luis Jose Alarcon-Aneiva and Nicoletta Fala},
  title     = {Real-Time Synchronization of Flight Simulation and Physiological Data Using Lab Streaming Layer: A Custom X-Plane Approach},
  booktitle = {Proceedings of the 23rd International Symposium on Aviation Psychology},
  year      = {2025},
  volume    = {23},
  pages     = {222--227},
  note      = {Wright State University},
  url       = {[https://corescholar.libraries.wright.edu/isap_2025/38/](https://corescholar.libraries.wright.edu/isap_2025/38/)}
}

```

---

## 🛠 Technical Specifications & Compatibility

The plugin is compiled for Windows systems using the X-Plane SDK. It utilizes a unique Stream ID (UID) per machine, allowing multiple simulators to operate on the same Local Area Network (LAN) without stream collisions.

| Binary | Architecture | SDK Version | X-Plane Version Compatibility |
| --- | --- | --- | --- |
| **`64/win.xpl`** | x64 | SDK 4.1 | X-Plane 11.x, 12.x (64-bit) |
| **`win.xpl`** | Win32 | SDK 2.1 | X-Plane 9.x, 10.x (32-bit) |

*Note: Both binaries are generated from the same source tree; only the Visual Studio configuration differs.*

---

## 🚀 Installation & Setup

### 1. Deployment

1. Download the latest release from the [Releases](https://www.google.com/search?q=https://github.com/aeon-lab/X-Plane-LSL-Implementation/releases) page.
2. Navigate to your X-Plane directory: `Resources/plugins/`.
3. Create a folder named `LSL_XPlane_Plugin`.
4. Place the appropriate binary (`win.xpl`) and the `config.txt` file into that folder.

### 2. Selecting Data Channels (Datarefs)

The plugin dynamically subscribes to flight variables defined in `config.txt`.

* Use `1` to enable a stream and `0` to disable it.
* **Example `config.txt`:**
```text
sim/flightmodel/position/latitude 1
sim/flightmodel/position/longitude 1
sim/flightmodel/position/elevation 1
sim/flightmodel/position/indicated_airspeed 1

```



### 3. Verification

* Launch X-Plane and navigate to **Plugins > Plugin Admin**.
* Verify that **LSL_XPlane_Plugin** is active and enabled.
* Consult the X-Plane `Log.txt` (located in the main X-Plane directory) to confirm the LSL stream has successfully initialized.

---

## 🌐 Network & Port Configuration

LSL relies on **Multicast UDP** and **TCP** for stream discovery and data transmission. In many academic or corporate lab environments, firewalls may block these ports by default.

To ensure the plugin can broadcast data to other computers (e.g., a dedicated recording PC), ensure the following ports are open on your Windows Firewall:

* **UDP Port 16571** (Multicast Discovery)
* **TCP Ports 16572–16600** (Data Transmission)

> **Pro Tip:** If you are using 3rd party security software (e.g., McAfee, Symantec, or Norton), you must manually whitelist the `X-Plane.exe` application to allow outbound LSL traffic.

---

## 📊 Data Acquisition

Once the plugin is running, the stream will be visible to any LSL-compatible receiver on the network.

### Recommended: LabRecorder

For high-fidelity data collection, we recommend using [LabRecorder](https://github.com/labstreaminglayer/App-LabRecorder). It captures and logs data from multiple LSL streams into a single `.xdf` file for perfectly synchronized post-hoc analysis.

### Real-time Analysis (Python)

You can access the stream programmatically via the `pylsl` library:

```python
from pylsl import StreamInlet, resolve_stream

# Resolve the 'Flight-Data' stream on the network
print("Looking for an X-Plane LSL stream...")
streams = resolve_stream('type', 'Flight-Data')

# Create a new inlet to read from the stream
inlet = StreamInlet(streams[0])

while True:
    # Pull a new sample from the simulator
    sample, timestamp = inlet.pull_sample()
    print(f"Timestamp: {timestamp} | Data: {sample}")

```

---

## ⚖️ License

This project is licensed under the **MIT License**.

## 🤝 Acknowledgments

* **[ÆON Lab](https://aeonresearch.org/), Auburn University** - PI: Dr. Nicoletta Fala.
* **X-Plane SDK** for the plugin framework.
* **Lab Streaming Layer (LSL)** for real-time data integration.
