## Windows Setup Guide (Docker/WSL)

> [!NOTE]
> Ensure that Docker Desktop is not installed; if so, uninstall and reboot before proceeding.

From the Microsoft store, install Windows Subsystem for Linux (WSL) \

From the Microsoft store, install Ubuntu 22.04 LTS \

Follow the setup to create your Ubuntu username and password.

From a Windows command prompt, paste the following:

`cd C:\WINDOWS\system32`

Then paste:

`wsl --setdefault Ubuntu-22.04`

From Windows apps, start Ubuntu 22.04, and paste the following inside the terminal:

```
sudo apt update
sudo apt upgrade -y
sudo mount --make-rshared /
```

> [!NOTE]
> `sudo mount --make-rshared` does not persist reboots, so it will need to be run each time WSL2 or Windows is restarted. Alternatively, see the [Ubuntu systemd service](https://github.com/I-am-PUID-0/DMB/wiki/FAQ#ubuntu-systemd-service) guide for automatically executing the command on startup for Ubuntu.

Follow the **[Docker](https://docs.docker.com/engine/install/ubuntu/)** install guide.

Follow the standard docker process for creating the container or follow the [Define the directory structure](https://github.com/I-am-PUID-0/DMB/wiki/Setup-Guides#define-the-directory-structure) and the remainder of the [Complete Beginners Guide](https://github.com/I-am-PUID-0/DMB/wiki/Setup-Guides#complete-beginners-guide)

To access the mount on Windows:
From the Ubuntu terminal, paste the following, including the punctuation:

`explorer.exe . `

A new file explorer window will appear; you’re now inside the Ubuntu directory structure

Navigate to the mount location and copy the full path from the explore window

From another file explorer window, click "This PC," then right-click in the space below the listed drives and select add a network location

In the pop-up, click next twice and past the mount location.

Follow the remaining prompted steps

Extra credit: install **[Portainer](https://docs.portainer.io/start/install-ce/server/docker/linux)**.
