# 5G Testbed Setup using USRP and srsRAN

This repository provides steps for setting up a 5G testbed using USRP devices with srsRAN, covering firmware setup and various network configurations, including two-machine setups and split-8 architecture with COTS UEs. Over-the-air configurations will be added soon.

## Steps for Setting Up USRP and Network Configurations

1. **Install UHD Libraries:**

   - Search and install the UHD libraries required for your USRP model. Ensure compatibility with your host machine and USRP firmware version.

2. **Insert Daughterboards:**

   - Carefully insert the appropriate daughterboards into the USRP. Ensure that they are securely fastened and correctly aligned.

3. **Connect USRP to Host Machine:**

   - Use a 1 Gigabit Ethernet patch cable to connect the USRP’s Ethernet port to the host machine's Ethernet port.

4. **Set IP Address for Ethernet Port:**

   - Configure the IP address of the Ethernet port on your host machine where the USRP is connected:
     - IP Address: `192.168.10.1`
     - Netmask: `255.255.255.0`
   - Ping the USRP to verify the connection:
     ```bash
     ping 192.168.10.2
     ```
   - Note: The default IP address of the USRP is `192.168.10.2`.

5. **Find USRP Device:**

   - Use the following command to list the details of the connected USRP device:
     ```bash
     sudo uhd_find_devices
     ```
   - This command will display the USRP model, serial number, and other details.

6. **Probe USRP and Update Firmware (if needed):**

   - Run the following command to probe the USRP:
     ```bash
     sudo uhd_usrp_probe
     ```
   - If prompted, burn a new firmware image onto the USRP as instructed in the console.

7. **Burn Image onto the USRP:**

   - Follow the commands that appear in the console to burn the appropriate image onto the USRP. Wait for the process to complete successfully.

8. **Restart the USRP:**

   - After burning the new image, power cycle (restart) the USRP to apply the changes.

9. **Verify USRP Setup:**
   - Run the probe command again to confirm the setup and log the USRP details:
     ```bash
     sudo uhd_usrp_probe
     ```
   - The details of the USRP, including firmware version, should now appear in the console.

## Network Configuration 1: Two Separate Machines

1. **USRP 1:**
   - Connect to the host machine running srsUE.
2. **USRP 2:**
   - Connect to a different machine running srsRAN gNB and 5G core.
3. **Interconnect USRPs:**
   - Connect the two USRPs using an SMA cable and a 30dB attenuator.
4. **Rationale:**
   - This setup is recommended if radio licensing is not available, as it avoids over-the-air transmissions.

## Network Configuration 2: Split Architecture with COTS UEs

1. **Will be added soon**
