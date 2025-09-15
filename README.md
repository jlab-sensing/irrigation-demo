# README

## Overview

This repository contains two Python scripts:

1. **`demoPullRequests.py`**  
   - A demonstration utility for handling and inspecting pull requests.  
   - Intended for testing workflows or interacting with pull request metadata in a controlled setup.  

2. **`remote_solenoid.py`**  
   - A remote control utility for an irrigation system’s solenoid valve.  
   - Communicates with an ESP32 device over HTTP to operate the solenoid, monitor soil moisture, and manage automatic irrigation.  

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
```bash
pip install pandas
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
- Provides full control over an irrigation solenoid connected to an ESP32.  
- Supports manual control, timed operations, and automatic irrigation based on soil moisture thresholds.
- IMPORTANT NOTE: The computer running the python script must be on the same WiFi network as the ESP32. In the case of jLab, that WiFi network is "HARE_Lab".

**Configuration**  
- Update the `ENTS_IP` constant in the script with the ESP32’s IP address. Example:  

```python
ENTS_IP = "172.31.105.241"
```

**Usage**

Run the script with command-line arguments:

```bash
python remote_solenoid.py <command> [options]
```

---

### Available Commands

#### Basic Control
- `open`  
  Open solenoid indefinitely.  
  ```bash
  python remote_solenoid.py open
  ```

- `close`  
  Close solenoid indefinitely.  
  ```bash
  python remote_solenoid.py close
  ```

- `timed [seconds]`  
  Open the solenoid for a specified duration (in seconds).  
  ```bash
  python remote_solenoid.py timed 300
  ```

- `state`  
  Check the current solenoid state.  
  ```bash
  python remote_solenoid.py state
  ```

#### Automatic Irrigation
- `auto_irrigation <min> <max>`  
  Enable automatic irrigation with custom thresholds and start monitoring.  
  Opens solenoid when moisture is below `<min>` and closes it when above `<max>`.  
  ```bash
  python remote_solenoid.py auto_irrigation 50 75
  ```

- `auto_on`  
  Enable automatic irrigation using previously set thresholds and start monitoring.  
  ```bash
  python remote_solenoid.py auto_on
  ```

- `auto_off`  
  Disable automatic irrigation and stop monitoring.  
  ```bash
  python remote_solenoid.py auto_off
  ```

- `set_thresholds <min> <max>`  
  Update soil moisture thresholds without starting auto irrigation.  
  ```bash
  python remote_solenoid.py set_thresholds 25 55
  ```

- `status`  
  Show the complete system status including solenoid state, thresholds, and auto mode.  
  ```bash
  python remote_solenoid.py status
  ```

- `moisture_check`  
  Query the ESP32 for the latest soil moisture reading.  
  ```bash
  python remote_solenoid.py moisture_check
  ```

---

### Examples

```bash
# Open solenoid for 5 minutes
python remote_solenoid.py timed 300

# Enable auto mode: open when <50%, close when >75%
python remote_solenoid.py auto_irrigation 50 75

# Update thresholds to 25–55% only
python remote_solenoid.py set_thresholds 25 55

# Enable automatic irrigation
python remote_solenoid.py auto_on

# Show full system status
python remote_solenoid.py status

# Check current moisture reading from ESP32
python remote_solenoid.py moisture_check
```

---

## Notes

- Ensure the ESP32 device is powered on, connected to the network, and running the irrigation firmware.  
- The IP address must be reachable from your machine.  
- `remote_solenoid.py` is a client-side utility: logic for soil moisture monitoring and auto-control runs on the ESP32.  

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

4. Run one of the commands to control or monitor the solenoid:  

   ```bash
   python remote_solenoid.py open
   python remote_solenoid.py timed 60
   python remote_solenoid.py auto_irrigation 40 70
   python remote_solenoid.py status
   ```

5. For pull request demo testing:  

   ```bash
   python demoPullRequests.py
   ```
