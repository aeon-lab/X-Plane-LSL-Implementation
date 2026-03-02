# X-Plane LSL Gateway: Real-Time Flight Data Synchronization

**Authors**: Luis Jose Alarcon-Aneiva & Nicoletta Fala (Auburn University, AEON Lab)  
**Contact**: [lja0024@auburn.edu](mailto:lja0024@auburn.edu) · [https://aeonresearch.org/](https://aeonresearch.org/)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![X-Plane SDK](https://img.shields.io/badge/X--Plane-SDK%204.1-blue)](https://developer.x-plane.com/sdk/)

This X-Plane plugin provides a high-performance bridge between the **X-Plane Flight Simulator** and the **Lab Streaming Layer (LSL)** ecosystem. It is specifically designed for researchers in human factors, neuroergonomics, and aviation psychology who require millisecond-accurate synchronization between flight telemetry and physiological data.

---

## 🔬 Proven Research Applications

This plugin was developed and validated at the **AEON Lab (Auburn University)** to solve complex data synchronization challenges in multi-modal flight studies.

### Revitalizing Legacy Hardware
A key advantage of this plugin is its ability to extract data from **older or traditional flight simulators** (like the PFC DCX MAX). Previously, these systems lacked native high-speed streaming or modern logging capabilities. This implementation allows researchers to bring "legacy" hardware into a modern LSL-synchronized pipeline without hardware modifications.

---

## 🛠 Technical Specifications & Compatibility

The plugin utilizes a unique Stream ID (UID) per machine, allowing multiple simulators to operate on the same LAN without stream collisions.

| Binary | Architecture | SDK Version | X-Plane Version Compatibility |
| :--- | :--- | :--- | :--- |
| **`64/win.xpl`** | x64 | SDK 4.1 | X-Plane 11.x, 12.x (64-bit) |
| **`win.xpl`** | Win32 | SDK 2.1 | X-Plane 9.x, 10.x (32-bit) |

---

## 🚀 Installation & Setup

### 1. Deployment
1. Download the latest release.
2. Navigate to your X-Plane directory: `Resources/plugins/`.
3. Create a folder named `LSL_XPlane_Plugin`.
4. Place the appropriate binary (`win.xpl`) and the `config.txt` file into that folder.

### 2. Selecting Data Channels (Datarefs)
X-Plane provides a vast array of flight data—from engine temperatures to control surface deflections—defined as **Datarefs**. This plugin can stream **any** available dataref by listing it in the `config.txt` file.

* **Find Datarefs:** To see a full list of available data and what each variable represents, consult the [Official X-Plane Dataref Directory](https://developer.x-plane.com/datarefs/).
* **Enable/Disable:** Use `1` to enable a stream and `0` to disable it.
* **Example `config.txt`:**
  ```text
  sim/flightmodel/position/latitude 1
  sim/flightmodel/position/longitude 1
  sim/flightmodel/position/elevation 1
  sim/flightmodel/position/indicated_airspeed 1

  ```

### 3. Verification

* Launch X-Plane and check **Plugins > Plugin Admin** to ensure **LSL_XPlane_Plugin** is active.
* Check the X-Plane `Log.txt` for the "LSL Stream Initialized" confirmation.

---

## 🌐 Network & Port Configuration

LSL relies on **Multicast UDP** and **TCP**. Ensure the following ports are open on your Windows Firewall to allow the plugin to broadcast to your recording PC:

* **UDP Port 16571** (Discovery)
* **TCP Ports 16572–16600** (Data)

*Note: If using 3rd party antivirus (McAfee/Symantec), you must manually whitelist `X-Plane.exe`.*

---

## 📊 Data Acquisition

### Recommended: LabRecorder

For research, use [LabRecorder](https://github.com/labstreaminglayer/App-LabRecorder) to capture the X-Plane stream alongside eye-tracking and heart rate data into a single `.xdf` file.

---

## 📚 Cite this work

If this plugin or the Lab Streaming Layer (LSL) framework facilitates your research, please cite the following:

### 1. Research Paper (This Plugin)
> Alarcon-Aneiva, L. J., & Fala, N. (2025). **Real-Time Synchronization of Flight Simulation and Physiological Data Using Lab Streaming Layer: A Custom X-Plane Approach.** *Proceedings of the 23rd International Symposium on Aviation Psychology*, 23, 222–227. [[Full Paper PDF](https://corescholar.libraries.wright.edu/isap_2025/38/)]

### 2. Lab Streaming Layer (LSL) Software Framework
> Kothe, C., Mullen, T., Xu, J., Maher, S., & Metting van Rijn, A. (2024). **Lab Streaming Layer (LSL)** [Computer software]. GitHub. https://github.com/sccn/labstreaminglayer

---

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

@software{Kothe_Lab_Streaming_Layer_2024,
  author = {Kothe, Christian and Mullen, Tim and Xu, Jinyi and Maher, Stephen and Metting van Rijn, AC},
  title = {{Lab Streaming Layer (LSL)}},
  url = {[https://github.com/sccn/labstreaminglayer](https://github.com/sccn/labstreaminglayer)},
  version = {1.16},
  year = {2024}
}
```

---

**License:** MIT · **Lab:** [AEON Lab, Auburn University](https://aeonresearch.org/)
