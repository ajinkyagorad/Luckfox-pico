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
- **SSH Login**: Invoke the following incantation to SSH into the device:
  ```sh
  ssh pico@172.32.0.70
  ```
- **Credentials**: Whisper the secret password `luckfox` to gain entry. 🔒✨

### Notes 📝🌿
- Ensure that your **firewall** is configured to allow connections on **port 22** (SSH). You can do this through Windows Firewall settings by creating an inbound rule. Let the path remain clear for your magic to flow. 🌠

### Troubleshooting ⚙️🛡️
- If you encounter any magical disturbances, ensure that the IP address and subnet mask are configured correctly.
- Check the USB connection, like a druid inspecting the strength of their vine, and confirm that the driver was properly installed.

You should now be able to access and control your Luckfox Pico via SSH over USB successfully. May the fox's magic and nature's wonders be with you on your quest! 🎉🦊✨

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

These steps will ensure you have internet sharing enabled while maintaining a reliable static IP to connect to your Pico. May the fox's magic guide you through! 🦊✨

### References 🔗📜
- [Luckfox Pico Image Burning Guide](https://wiki.luckfox.com/Luckfox-Pico/Linux-MacOS-Burn-Image)
- [Luckfox Pico SSH/Telnet Login Guide](https://wiki.luckfox.com/Luckfox-Pico/SSH-Telnet-Login)
