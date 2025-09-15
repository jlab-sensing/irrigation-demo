# README

## Overview

This repository contains two Python scripts:

1. **`demoPullRequests.py`**  
   - A demonstration utility for handling and inspecting pull requests.  
   - Intended for testing workflows or interacting with pull request metadata in a controlled setup.  

2. **`remote_solenoid.py`**  
   - A remote control utility for an irrigation system’s solenoid valve.  
   - Communicates with an ESP32 device over HTTP to **open**, **close**, or **schedule timed operations** of the solenoid.  

Both scripts are designed for testing, automation, and demonstration purposes.

---

## Requirements

- Python **3.8+**  
- Installed dependencies (see below)  

Install dependencies:  

```bash
pip install -r requirements.txt
```

If no `requirements.txt` exists, you may need:  

```bash
pip install requests
```

---

## Files

### 1. `demoPullRequests.py`

**Purpose**  
- Demonstrates interaction with pull request data.  
- Useful for showcasing GitHub-like workflows or simulated testing.  

**How to Run**

```bash
python demoPullRequests.py
```

**Expected Behavior**  
- Prints structured information about pull requests.  
- May display metadata such as title, description, author, and status.  
- Can be extended for custom PR testing pipelines.  

---

### 2. `remote_solenoid.py`

**Purpose**  
- Allows remote control of an irrigation solenoid valve connected to an ESP32.  
- Supports three main modes:
  - **Open indefinitely**  
  - **Close indefinitely**  
  - **Open for a timed duration**  

**Configuration**  
- Update the `ENTS_IP` constant in the script with the ESP32’s IP address. In jLab, this address is already set to the correct IP used with the WiFi network in the back garden. Example:  

```python
ENTS_IP = "172.31.105.241"
```

**Usage**

Run the script with command-line arguments:

```bash
python remote_solenoid.py <command> [duration]
```

**Commands**

- `open`  
  Opens the solenoid indefinitely.  

  ```bash
  python remote_solenoid.py open
  ```

- `close`  
  Closes the solenoid indefinitely.  

  ```bash
  python remote_solenoid.py close
  ```

- `open_for <seconds>`  
  Opens the solenoid for a specific time (in seconds).  

  ```bash
  python remote_solenoid.py open_for 30
  ```

- `auto_on`  
  Enables automatic irrigation mode controlled by ESP32 logic.  

  ```bash
  python remote_solenoid.py auto_on
  ```

- `auto_off`  
  Disables automatic irrigation mode.  

  ```bash
  python remote_solenoid.py auto_off
  ```

**Example Output**

```
Automatic irrigation enabled
Response: Auto enabled
Streaming sen0308 humidity data from last 30 seconds...
Sent initial moisture reading: 62.5%

============================================================
SYSTEM STATUS SUMMARY
============================================================
Current Soil Humidity: 62.5%
Solenoid State: CLOSED
Auto Irrigation: ENABLED
```

---

## ⚠Notes

- Ensure the ESP32 device is powered on, connected to the network, and running the irrigation firmware.  
- The IP address must be reachable from your machine.  
- `remote_solenoid.py` is a **client-side utility**: logic for soil moisture monitoring and auto-control runs on the ESP32.  

---

## Quick Start

1. Clone the repository:  

   ```bash
   git clone <repo_url>
   cd <repo_name>
   ```

2. Install dependencies:  

   ```bash
   pip install requests
   ```

3. Update the ESP32 IP in `remote_solenoid.py`.  

4. Run one of the commands to control the solenoid:  

   ```bash
   python remote_solenoid.py open
   python remote_solenoid.py open_for 60
   python remote_solenoid.py auto_on
   ```

5. For pull request demo testing:  

   ```bash
   python demoPullRequests.py
   ```
