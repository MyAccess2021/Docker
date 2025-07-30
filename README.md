# Docker and Docker Compose Installation Guide (Ubuntu/Debian)

This guide will help you install the Docker Engine, configure your system for non-root Docker usage, and install Docker Compose as a standalone binary.

## 1. Remove Older Docker Versions

If you have any previous Docker installations, remove them:
```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

## 2. Update the Package Index and Install Dependencies

Update your package index and install required tools:
```bash
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

## 3. Add Docker’s Official GPG Key

Create the keyrings directory and add Docker’s GPG key:
```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

## 4. Add Docker’s Official Repository

Set up the Docker repository:
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## 5. Install Docker Engine and Containerd

Update again and install Docker:
```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
```

## 6. Enable and Start Docker Service

Enable Docker to start on boot, and run it now:
```bash
sudo systemctl enable docker
sudo systemctl start docker
```

## 7. Allow Non-root Access to Docker

Add your user to the `docker` group:
```bash
sudo usermod -aG docker $USER
newgrp docker
```
> **Tip:** You may need to log out and log back in for this to fully take effect.

## 8. Install Docker Compose (Standalone Binary)

Download Docker Compose to your system, give it execute permissions, and make sure it is available in your `PATH`.

```bash
sudo curl -SL "https://github.com/docker/compose/releases/download/v2.29.1/docker-compose-linux-x86_64" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```
> **Note:** Change the Compose version URL as new versions are available: [https://github.com/docker/compose/releases](https://github.com/docker/compose/releases)

## 9. Verify Installation

Check that Docker and Docker Compose work:
```bash
docker --version
docker-compose --version
docker ps
```

## 10. (Optional) To Use Docker Compose as a Plugin

Instead of the above Compose install, you can use the plugin version:

```bash
sudo apt-get install docker-compose-plugin
```
Using Docker's Official Installation Script
1. Run the installation script:

```bash
sudo curl -SL https://github.com/docker/compose/releases/download/v2.29.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
```
Make the binary executable:

```bash
sudo chmod +x /usr/local/bin/docker-compose
```
And then use:
```bash
docker compose version
```

## References

- [Docker CE Install Docs](https://docs.docker.com/engine/install/ubuntu/)
- [Docker Compose Install Docs](https://docs.docker.com/compose/install/standalone/)
- [Docker Compose Releases](https://github.com/docker/compose/releases)

**You now have Docker and Docker Compose ready for use on your Ubuntu/Debian system!**  
Feel free to copy/paste these sections into your project README or IT documentation.
