# Luckfox Pico SSH Setup via USB 🦊🌿✨

Welcome, brave traveler, to the magical realm of Luckfox Pico. This guide will lead you step-by-step on your quest to set up your Luckfox Pico device and access it via SSH over a USB connection. Let the magic of nature and technology blend in harmony! 🍃✨

### 1. Install Luckfox Driver 🛠️🦊

- **Download the Driver**: Journey to the official Luckfox website and retrieve the mystical driver that grants you USB access to your device. [🔗 Official Driver Download](#)
- **Install the Driver**: Run the enchanted installer to set up the USB RNDIS (Remote Network Driver Interface Specification) driver on your Windows PC, bringing the powers of connectivity to life.

### 2. Download and Install Luckfox Image 💾🗺️

- **Download Image**: Head to the sacred Luckfox site to download the Luckfox Pico Mini image (Ubuntu version). [Luckfox Pico Image Download](https://wiki.luckfox.com/Luckfox-Pico/Linux-MacOS-Burn-Image)
- **Prepare SD Card**: Take a 64GB microSD card, the vessel of your image, and format it with **FAT32** or **exFAT**—ensuring it is ready for the journey. 🌀
- **Flash the Image**: Use the **SocToolKit**, a powerful tool forged by the engineers of Luckfox, to burn the image onto the SD card. Refer to the sacred burning guide [here](https://wiki.luckfox.com/Luckfox-Pico/Linux-MacOS-Burn-Image).
- **Insert the SD Card**: With the image now imbued upon it, place the SD card into your Luckfox Pico—like a key into an ancient gateway. 🗝️

### 3. Set Up Network on Windows 🖧🌲

- **Connect the Pico via USB**: Connect your Luckfox Pico to your PC using a USB cable, as if bridging two worlds with a single thread of magic.
- **Configure RNDIS Network**: Open the mystical portal on your PC:
  - Navigate to **Settings** -> **Network & Internet** -> **Advanced Network Settings** -> **Change Adapter Options**.
  - Locate the "Remote NDIS based Internet Sharing Device"—a hidden relic.
  - Right-click, select **Properties**, then double-click **Internet Protocol Version 4 (TCP/IPv4)**.
  - Assign the **IPv4 address** to `172.32.0.100` and the **Subnet Mask** to `255.255.0.0` to align with the magic of the network. 🌌

### 4. Access the Device via SSH 🔑🦉

- **Open a Terminal**: Open **PowerShell** or your preferred terminal, like summoning your familiar to aid in your spellwork. 🧙‍♂️
- **SSH Login**: Run the following command to SSH into the device:
  ```sh
  ssh pico@172.32.0.70
  ```
- **Credentials**: Whisper your newly set secret password to gain entry. 🔒✨

### Notes 📝🌿

- Ensure that your **firewall** is configured to allow connections on **port 22** (SSH). You can do this through Windows Firewall settings by creating an inbound rule. Let the path remain clear for your magic to flow. 🌠

### Troubleshooting ⚙️🛡️

- If you encounter any magical disturbances, ensure that the IP address, subnet mask, and swap space are configured correctly.
- Ensure there is enough swap space to support package installations, especially if you encounter memory-related errors. See the swap section below for more details.
- Check the USB connection, like a druid inspecting the strength of their vine, and confirm that the driver was properly installed.

You should now be able to access and control your Luckfox Pico via SSH over USB successfully. Congratulations! You should now be able to access and control your Luckfox Pico via SSH over USB successfully. 🎉

### Additional Section: Enabling ICS and Setting a Static IP 🌐🦊✨

If you want to share your laptop's internet with your Pico, you can enable **Internet Connection Sharing (ICS)**. However, enabling ICS may change the default IP, making it hard to reconnect. Here are steps to maintain a static IP:

1. **Enable Internet Connection Sharing**:

   - **Go to WiFi Properties** on your laptop (`Win + R`, type `ncpa.cpl`).
   - **Right-click on your WiFi connection**, select **Properties**, and navigate to the **Sharing** tab.
   - Check **"Allow other network users to connect through this computer's Internet connection"**.
   - Click **Yes** when prompted that the IP will change to `192.168.137.1`.

2. **Set a Static IP on the Pico Before Enabling ICS**:

   - First, **SSH into your Pico** using the initial IP (`ssh pico@172.32.0.70`).
   - Once inside, edit the network configuration file to set a static IP in the ICS range:
     ```sh
     sudo nano /etc/network/interfaces
     ```
     - Modify the settings as follows:
       ```sh
       auto usb0
       iface usb0 inet static
       address 192.168.137.2
       netmask 255.255.255.0
       gateway 192.168.137.1
       ```
   - Save and apply the changes:
     ```sh
     sudo ifdown usb0 && sudo ifup usb0
     ```

3. **SSH Using the New Static IP**:

   - After enabling ICS, **SSH to the new static IP**:
     ```sh
     ssh pico@192.168.137.2
     ```

These steps will ensure you have internet sharing enabled while maintaining a reliable static IP to connect to your Pico. 

### Adding Swap Space for Smooth Performance 💾🌀✨

To ensure smooth performance when running resource-intensive tasks or installations on the Pico, it is recommended to create a swap file. A swap file acts as additional virtual memory that the system can use when the physical RAM is insufficient, helping prevent crashes or slowdowns during heavy operations.

1. **Create a Swap File**:

   ```sh
   sudo fallocate -l 1.5G /swapfile
   ```

   - If `fallocate` fails, use `dd` instead:

   ```sh
   sudo dd if=/dev/zero of=/swapfile bs=1M count=1536
   ```

2. **Set Permissions**:

   ```sh
   sudo chmod 600 /swapfile
   ```

3. **Set Up the Swap File**:

   ```sh
   sudo mkswap /swapfile
   sudo swapon /swapfile
   ```

4. **Verify Swap**:

   ```sh
   sudo swapon --show
   ```

   This will help ensure your Pico has enough virtual memory to handle tasks and installations without running into memory issues.

### Install Useful Packages in One Command 🛠️🦊✨

To make your Pico more versatile, you can install several useful packages with a single command. These packages include essential tools like Python, Git, Node.js, and others to enhance the Pico's capabilities:

```sh
sudo apt-get update && sudo apt-get install -y python3 git nodejs npm tightvncserver net-tools
```

This command will install:

- **Python 3**: For scripting and automation.
- **Git**: To manage and clone repositories.
- **Node.js & npm**: For running JavaScript applications and managing packages.
- **TightVNC Server**: To allow remote GUI access.
- **Net-tools**: To provide useful networking utilities.

May your Pico be powerful and ready for all the adventures ahead! 🎉🦊✨

### References 🔗📜

- [Luckfox Pico Image Burning Guide](https://wiki.luckfox.com/Luckfox-Pico/Linux-MacOS-Burn-Image)
- [Luckfox Pico SSH/Telnet Login Guide](https://wiki.luckfox.com/Luckfox-Pico/SSH-Telnet-Login)

