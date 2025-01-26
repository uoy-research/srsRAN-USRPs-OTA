# **5G Testbed Setup Using USRPs, srsRAN, and srsUE**

This repository provides detailed instructions to set up a 5G testbed using two USRP X310 devices, leveraging the srsRAN stack for the gNB, 5G core, and srsUE.

---

## **Overview of the Architecture**

![Testbed Architecture](https://docs.srsran.com/projects/project/en/latest/_images/gNB_srsUE_usrp.png)

- **First PC**:

  - Connected to a USRP X310 via a 1 Gbps Ethernet link
  - Running the gNB and 5G Core

- **Second PC**:

  - Connected to another USRP X310 via a 1 Gbps Ethernet link
  - Running srsUE

- **Synchronization**:  
  Both USRPs are synchronized and clocked using a CDA-2990 G clock distribution module and communicate via antennas.

---

## **Steps for Setting Up USRP X310**

### 1. **Install UHD Libraries**

- Download and install the UHD libraries compatible with your USRP model and firmware version.
- Refer to the official [UHD installation guide](https://github.com/EttusResearch/uhd) for details.

### 2. **Insert Daughterboards**

- Ensure the correct daughterboards (e.g., UBX-160) are securely installed and properly aligned in the USRP.

### 3. **Connect USRP to Host Machine**

- Use a 1 Gbps Ethernet cable to connect the USRP’s Ethernet port to the host machine's Ethernet port.

### 4. **Configure Ethernet Port IP Address**

- Set the IP address of the Ethernet port connected to the USRP:

  - **IP Address**: `192.168.10.1`
  - **Netmask**: `255.255.255.0`

- Verify the connection by pinging the USRP’s default IP address (`192.168.10.2`):
  ```bash
  ping 192.168.10.2
  ```

### 5. **Detect USRP Device**

- Run the following command to identify the connected USRP:
  ```bash
  sudo uhd_find_devices
  ```
- This will display details like the model, serial number, and IP configuration.

### 6. **Probe USRP and Update Firmware**

- Probe the USRP to verify connectivity and firmware version:
  ```bash
  sudo uhd_usrp_probe
  ```
- If required, update the firmware by following the instructions provided in the console.

### 7. **Burn Firmware Image**

- Use the commands suggested in the console output to burn the appropriate firmware image.
- Wait until the process completes successfully.

### 8. **Restart USRP**

- Power cycle the USRP to ensure the firmware changes are applied.

### 9. **Verify the Setup**

- Confirm the setup by probing the USRP again:
  ```bash
  sudo uhd_usrp_probe
  ```
- Check for accurate firmware details and operational status.

---

## **Code**

This repository includes the config files for srsUE and gNB. It also includes a patch provided to us by the srsRAN team to make this setup work with USRP x310s. Add this patch in the srsRAN_4G folder and run.

```bash
git apply fix_prach.patch
```

Check the changes to ensure they were applied correctly:

```bash
git status
git diff
```

Finally, build the srsRAN_4G folder
