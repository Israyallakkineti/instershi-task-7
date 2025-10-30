# 🧠 Task 7 – Monitor System Resources Using Netdata

## 🎯 Objective
Install **Netdata** and visualize **system and application performance metrics** using Docker.  
Understand lightweight monitoring for servers, containers, and applications in real time.

---

## 🛠 Tools Used
- **Netdata** (Free, open-source monitoring tool)
- **Docker**
- **Ubuntu (AWS EC2 Instance)**

---

## ⚙️ Setup & Implementation

### 🧩 Step 1: Update the System
```bash
sudo apt update && sudo apt upgrade -y

Step 2: Install Docker


sudo apt install ca-certificates curl gnupg lsb-release -y
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y

Verify Docker:---------------

docker --version
sudo systemctl enable docker
sudo systemctl start docker


Step 3: Run Netdata in Docker :----------------

docker run -d --name=netdata \
  -p 19999:19999 \
  --cap-add SYS_PTRACE \
  --security-opt apparmor=unconfined \
  -v netdataconfig:/etc/netdata \
  -v netdatalib:/var/lib/netdata \
  -v netdatacache:/var/cache/netdata \
  -v /etc/passwd:/host/etc/passwd:ro \
  -v /etc/group:/host/etc/group:ro \
  -v /proc:/host/proc:ro \
  -v /sys:/host/sys:ro \
  -v /etc/os-release:/host/etc/os-release:ro \
  netdata/netdata


Check container status:-----------------------------

docker ps
http://<your-public-IP>:19999

EC2 -SECURTIY-SECURITY GROUP-INBOUND RULE -EDIT -TYPE : CUSTOME TCP -PORT : [1999] -SOURCE [ANYWHEREIP4] -SAVE

http://<your-public-IP>:19999




