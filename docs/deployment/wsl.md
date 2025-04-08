---
title: Deploy with WSL
---

## 🖥️ Deploying DMB on Windows Setup Guide (Docker/WSL)

!!! warning "Docker Desktop"
    Ensure that Docker Desktop is not installed; if so, uninstall and reboot before proceeding.

This guide will walk you through setting up DMB on a Windows system using a **lightweight Docker + WSL2 setup**, without relying on Docker Desktop. 

----

### 🐧 WSL Install

1. From the Microsoft store, install Windows Subsystem for Linux (WSL)

2. From the Microsoft store, install Ubuntu 22.04 LTS

3. Follow the setup to create your Ubuntu username and password

4. From a Windows command prompt, paste the following:

    ```bash
    cd C:\WINDOWS\system32
    ```

5. Then paste:

    ```bash
    wsl --setdefault Ubuntu-22.04
    ```

6. From Windows apps, start Ubuntu 22.04, and paste the following inside the terminal:

    ```bash
    sudo apt update
    sudo apt upgrade -y
    sudo mount --make-rshared /
    ```

!!! note 
     `sudo mount --make-rshared` does not persist reboots, so it will need to be run each time WSL2 or Windows is restarted. Alternatively, see the [Ubuntu systemd service](../faq/rclone.md#ubuntu-systemd-service) guide for automatically executing the command on startup for Ubuntu.

----

### 🐳 Docker Install

1. Follow the **[Docker](https://docs.docker.com/engine/install/ubuntu/)** install guide.

2. Follow the standard docker process for creating the container or follow the [Docker Deployment](docker.md) or [Portainer Deployment](portainer.md) guides

----

### 📂 Accessing the Mount on Windows

1. From the Ubuntu terminal, paste the following, including the punctuation:

    ```bash 
    explorer.exe . 
    ```

2. A new file explorer window will appear; you’re now inside the Ubuntu directory structure

3. Navigate to the mount location and copy the full path from the explore window

4. From another file explorer window, click "This PC," then right-click in the space below the listed drives and select add a network location

5. In the pop-up, click next twice and past the mount location.

6. Follow the remaining prompted steps


### 🌐 Mirrored Mode Networking

Starting with **Windows 11 22H2**, WSL2 supports a new networking mode called **mirrored networking**, which improves compatibility and unlocks several new features by mirroring Windows' network interfaces into Linux.

#### ✅ Benefits of Mirrored Networking

- 🧭 Full **IPv6** support  
- 🔁 Access **Windows services** from WSL using `127.0.0.1`  
- 🔒 Improved VPN support (VPNs work in both Windows and WSL)  
- 📡 Multicast compatibility  
- 🧷 Reach WSL directly from your **local LAN**

---

#### 🔧 Enabling Mirrored Mode

1. Open (or create) the `.wslconfig` file in your Windows home directory:

```powershell
notepad $env:USERPROFILE\.wslconfig
```

2. Add the following section:

```ini
[wsl2]
networkingMode=mirrored
```

3. Restart WSL for the changes to take effect:

```bash
wsl --shutdown
```

Then restart your distro from the Windows menu or run:

```bash
wsl
```

---

#### 📌 Additional Notes

- You can combine this with [`autoProxy=true`](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#configuration-settings-for-wslconfig) if you're using a proxy.
- This setting applies globally across all WSL2 instances.



### 🌟 Extra Credit

If you want to manage Docker visually via Portainer:

1. Create the Portainer data volume:
    ```bash
    docker volume create portainer_data
    ```

2. Start the Portainer container:

    ```bash
    docker run -d \
    -p 8000:8000 \
    -p 9443:9443 \
    --name portainer \
    --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data \
    portainer/portainer-ce:latest
    ```

You can now manage Docker containers via the browser at: `https://<ip>:9443`

!!! note 
    On the first run of Portainer, you need to access the Web UI quickly to create your initial administrator user, which is crucial for accessing and managing your Docker environment. 
    
!!! tip
    If you can't access the UI after the initial setup, ensure the Portainer container is running and that the correct port is open. 
    You might need to restart the container if it timed out. 

For more, see the [Portainer Deployment Guide](./portainer.md).

---

Now you’re ready to run DMB inside WSL2 with full Docker support — no Docker Desktop required!
