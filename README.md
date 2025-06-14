# 🔐 Splunk Log Monitoring Setup on Ubuntu

This project demonstrates the full implementation of **Splunk Enterprise** and **Splunk Universal Forwarder** on Ubuntu for centralized log collection, real-time monitoring, and analysis — essential for building foundational SOC (Security Operations Center) skills.

---

## 🖥️ Tools Used:
- **Splunk Enterprise** (installed on Windows as central server)
- **Splunk Universal Forwarder** (installed on Ubuntu)
- **Ubuntu Server** (client machine via VirtualBox)
- **PuTTY** (for SSH access)
- **Firewall Configuration** (Port 9997/TCP for log forwarding)

---

## 🛠️ Step-by-Step Implementation

### 1️⃣ Install Splunk Enterprise (Server Side)
- Sign up and download from: https://www.splunk.com/en_us/download/splunk-enterprise.html
- Install Splunk on Windows and create admin credentials
- Access dashboard at: `http://localhost:8000`

### 2️⃣ Setup Ubuntu Server (Client Side)
- Install Ubuntu using VirtualBox
- SSH into the server using PuTTY

### 3️⃣ Install Splunk Universal Forwarder on Ubuntu
```bash
sudo ufw allow 22/tcp
sudo ufw allow 9997/tcp

# Download and install the forwarder
wget https://download.splunk.com/products/universalforwarder/releases/9.4.3/linux/splunkforwarder-9.4.3-linux-amd64.deb
sudo dpkg -i splunkforwarder-9.4.3-linux-amd64.deb
```

### 4️⃣ Connect Forwarder to Splunk Server
```bash
cd /opt/splunkforwarder/bin
sudo ./splunk start --accept-license
sudo ./splunk enable boot-start
sudo ./splunk add forward-server [SPLUNK-SERVER-IP]:9997 -auth admin:admin
sudo ./splunk add monitor /var/log/auth.log -auth admin:admin
sudo ./splunk restart
```

### 5️⃣ Enable Receiving on Splunk Enterprise Server
- Go to **Settings → Forwarding & Receiving → Configure Receiving**
- Add **Port 9997** as the receiving port

---

## ✅ Output:
- Logs from the Ubuntu server are visible on Splunk Enterprise under **Search & Reporting**
- Navigate to `Search → Data Summary → Hosts` to view logs from Universal Forwarder


## 📄 Author
**Afroz Shaikh**  
📧 afrozshaikh8086@gmail.com  
📅 Project: SOC Training (Splunk Implementation)  
