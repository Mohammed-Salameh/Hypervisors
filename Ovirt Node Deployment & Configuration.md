### Step 1: Access Server Management
- Access the server's Integrated Lights Out (ILO) or Integrated Dell Remote Access Controller (IDRAC) interface, depending on whether you are using an HP server or a Dell server respectively.

### Step 2: Access Remote Console
- Navigate to the remote console option in ILO/IDRAC to remotely view and interact with the server's screen.

### Step 3: Attach oVirt Node ISO
- Use the remote console's options to virtually attach the oVirt Node ISO to the server as if it were physically present.

### Step 4: Boot Sequence
- Reboot the server.
- During the server's boot-up process, press F11 (or the appropriate key based on your server's brand/model) to access the boot menu.

### Step 5: Select Boot Device
- In the boot menu, choose the CD/ROM option, which is typically the first option in the list. This will tell the server to boot from the oVirt Node ISO you attached.

### Step 6: Start oVirt Node Installation
- Once the ISO content is loaded, you'll see several boot options. Choose the option for "oVirt 4.5.4 Node" to begin the installation process.

### Step 7: Disk Configuration
- During the installation, you'll be prompted to select a destination disk. Choose "/dev/sda" or the appropriate disk identifier if different.

### Step 8: Root Password Configuration
- Configure and confirm a strong password for the root user. This password will be used to administer the server post-installation.

### Step 9: Network Configuration
- After the installation completes:
# 1. Access the server's terminal (either directly or through the remote console).
# 2. Type `nmtui` to open the NetworkManager Text User Interface.
# 3. Select "Edit a connection".
# 4. Choose your management network interface from the list.
# 5. Set up a static IP address, netmask, gateway, and DNS for this interface.
# 6. Configure the hostname for the oVirt Node.
# 7. Save your changes and exit `nmtui`.

## Step 10: Reboot
# After making all the necessary configurations, reboot the server to ensure all settings take effect.

# Once the server is back online, you can proceed with further configurations or adding the node to an oVirt engine.
