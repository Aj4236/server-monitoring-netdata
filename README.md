# Task 7: Monitor System Resources Using Netdata on AlmaLinux

## Objective
Install and configure Netdata to **monitor and visualize system and application performance metrics** in real-time on AlmaLinux.

---

## Tools Used
- **Netdata** – Open-source monitoring tool  
- **Docker** – Container platform for running Netdata

---

## Features Monitored
- CPU usage per core  
- Memory and swap usage  
- Disk I/O (read/write rates)  
- Network traffic  
- Docker containers (if any)  
- System alerts and logs

---

## Setup Instructions

### 1. Install Docker on AlmaLinux
```bash
# Remove any old Docker versions
sudo yum remove docker \
                docker-client \
                docker-client-latest \
                docker-common \
                docker-latest \
                docker-latest-logrotate \
                docker-logrotate \
                docker-engine -y

# Install dependencies
sudo yum install -y yum-utils

# Add Docker repository
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# Install Docker
sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Start and enable Docker
sudo systemctl start docker
sudo systemctl enable docker

# Add your user to Docker group (optional, allows running Docker without sudo)
sudo usermod -aG docker $USER
Log out and log back in for group changes to take effect.

2. Run Netdata Container
# Using sudo (or if user added to docker group, sudo is optional)
sudo docker run -d \
  --name=netdata \
  -p 19999:19999 \
  --cap-add=SYS_PTRACE \
  --security-opt apparmor=unconfined \
  netdata/netdata
3. Access Netdata Dashboard
Remote access via IP server via browse:
http://192.168.153.135:19999
4. Firewall Setup (if needed)
# Allow Netdata HTTP port
sudo firewall-cmd --permanent --add-port=19999/tcp

# Reload firewall
sudo firewall-cmd --reload
Logs Location
/var/log/netdata
Screenshot Deliverables
Include screenshots of:

CPU & Memory graphs

Disk & Network graphs

Docker container metrics (if any)

Outcome
This setup provides a lightweight, real-time monitoring solution for system resources and Docker containers on AlmaLinux. Alerts and logs can be monitored directly from the Netdata dashboard
