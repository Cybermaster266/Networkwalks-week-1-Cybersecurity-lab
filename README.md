# NETWORKWALKS B084 – Week 1 Project
## Cybersecurity Lab Setup Using Kali Linux and VirtualBox

### 1. Project Overview
This project involved setting up a Kali Linux virtual machine using Oracle VirtualBox for cybersecurity practice. I cloned my existing Kali Linux virtual machine and configured the clone to use a NAT Network.

### 2. Lab Environment
- **Host OS:** Windows
- **Virtualization Software:** Oracle VirtualBox
- **Guest OS:** Kali Linux 2026.2
- **Network Type:** NAT Network
- **NAT Network Name:** NatNetwork
- **IPv4 Subnet:** `10.0.0.0/24`
- **Static IP Address:** `10.0.0.2/24`
- **Gateway:** `10.0.0.1`
- **DNS Server:** `8.8.8.8`

### 3. Tasks Performed
1. Created a clone of the existing Kali Linux virtual machine.
2. Configured a NAT Network in VirtualBox.
3. Set the NAT Network IPv4 prefix to `10.0.0.0/24`.
4. Attached the cloned Kali Linux VM to the NAT Network.
5. Configured the network connection to use a static IPv4 address.
6. Troubleshot the network connection when internet access failed.

### 4. IP Address Configuration

The intended network settings were:

| Setting | Value |
|---|---|
| IPv4 Method | Manual |
| IP Address | `10.0.0.2/24` |
| Gateway | `10.0.0.1` |
| DNS | `8.8.8.8` |
| Network Interface | `eth0` |

### 5. Problem Faced: Internet Access

After connecting the cloned Kali Linux VM to the NAT Network, internet access was unavailable. The `eth0` interface did not display an assigned IP address, and NetworkManager reported that connection activation failed because the IP configuration could not be reserved.

### 6. Troubleshooting and Solution

I used NetworkManager (`nmcli`) to associate the connection with the `eth0` interface and reapply the static IP configuration.

**Step 1: Associate the connection with `eth0`.**

```bash
sudo nmcli connection modify "Wired connection 1" connection.interface-name eth0
```

**Step 2: Reapply the static IP settings.**

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.method manual ipv4.addresses 10.0.0.2/24 ipv4.gateway 10.0.0.1 ipv4.dns 8.8.8.8
```

**Step 3: Configure the duplicate-address detection timeout.**

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

**Step 4: Restart the connection.**

```bash
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

**Step 5: Check the IP address.**

```bash
ip addr show eth0
```

**Step 6: Test internet connectivity.**

```bash
ping -c 4 8.8.8.8
```

The commands above document the troubleshooting steps attempted. The final IP assignment and internet connectivity should be verified before marking the issue as resolved.

### 7. Skills Practised
- Virtual machine cloning and configuration
- VirtualBox NAT Network setup
- Static IPv4 addressing
- Linux network interface troubleshooting
- NetworkManager command-line administration
- Basic connectivity testing

### 8. Conclusion
This project provided practical experience configuring a Kali Linux virtual machine for cybersecurity labs and troubleshooting network connectivity issues. It also reinforced the importance of correctly configuring IP addresses, gateways, DNS settings, and network interfaces.

*Author*
Samuel Ariyo 

**Project:** NETWORKWALKS B084 Cybersecurity Lab Setup  
**Week:** 1
