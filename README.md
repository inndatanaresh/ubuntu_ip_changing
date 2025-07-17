# IP Address Configuration in Ubuntu Using Netplan

This document outlines the steps to configure or change a static IP address on an Ubuntu system using Netplan.

## Prerequisites

* Ensure you have root or sudo access.
* Identify the correct network interface name (e.g., `ens18`).
* Backup existing Netplan configuration files before making changes.

## Step 1: Edit the Netplan Configuration File

Open the Netplan configuration file. The location may vary; common paths include:

```bash
sudo nano /etc/netplan/01-netcfg.yaml
```

Or

```bash
sudo nano /etc/netplan/50-cloud-init.yaml
```

Example configuration content:

```yaml
network:
  ethernets:
    ens18:
      addresses:
        - 10.10.5.50/24
      gateway4: 10.10.5.1
      nameservers:
        addresses:
          - 8.8.8.8
  version: 2
```

* Replace `ens18` with your actual network interface name if different.
* Adjust the `addresses`, `gateway4`, and `nameservers` values as needed.

## Step 2: Apply the Configuration

After saving the file, apply the changes using Netplan:

```bash
sudo netplan apply
```

## Step 3: Verify the IP Configuration

Check the applied network settings:

```bash
ip addr show ens18
```

Or test connectivity:

```bash
ping 8.8.8.8
```

---

**Notes:**

* Syntax errors in Netplan YAML files will prevent configuration from applying. Validate the syntax carefully.
* For troubleshooting, use:

```bash
sudo netplan try
```

* If issues occur, revert to the backup configuration file.
