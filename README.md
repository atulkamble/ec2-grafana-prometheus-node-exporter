# grafana-server
Grafana Server
```
// installation of grafana server 

t3.medium | SG-Inbound-3000 | 9090

sudo yum update -y 
sudo yum install -y https://dl.grafana.com/grafana-enterprise/release/12.2.1/grafana-enterprise_12.2.1_18655849634_linux_amd64.rpm
sudo systemctl start grafana-server
sudo systemctl enable  grafana-server
sudo systemctl status grafana-server

http://18.232.59.17:3000/

>> admin,admin

>> Admin@123

// install prometheus 

wget https://prometheus.io/download/3.7.3/2025-10-29/prometheus-3.7.3.linux-amd64.tar.gz

sudo yum install collectd-write_prometheus.x86_64 -y

scp -i /Users/atul/Downloads/garafana.pem \
/Users/atul/Downloads/prometheus-3.7.3.linux-amd64.tar.gz \
ec2-user@18.232.59.17:/home/ec2-user/

sudo tar -xvf prometheus-3.7.3.linux-amd64.tar.gz 
```

# **🔹 3. Install Required Packages**

```sh
sudo yum update -y
sudo yum install wget tar -y
```

---

# **🔹 4. Download Prometheus**

(Use the latest version from Prometheus downloads)

```sh
cd /opt
sudo wget https://github.com/prometheus/prometheus/releases/download/v2.51.2/prometheus-2.51.2.linux-amd64.tar.gz
```

---

# **🔹 5. Extract the Tar File**

```sh
sudo tar -xvf prometheus-2.51.2.linux-amd64.tar.gz
sudo mv prometheus-2.51.2.linux-amd64 prometheus
```

---

# **🔹 6. Create Prometheus User**

```sh
sudo useradd --no-create-home --shell /bin/false prometheus
```

---

# **🔹 7. Move Binaries to /usr/local/bin**

```sh
cd /opt/prometheus
sudo cp prometheus /usr/local/bin/
sudo cp promtool /usr/local/bin/
```

---

# **🔹 8. Configure Prometheus Directory**

```sh
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
sudo cp -r consoles /etc/prometheus
sudo cp -r console_libraries /etc/prometheus
sudo cp prometheus.yml /etc/prometheus/
```

---

# **🔹 9. Set Permissions**

```sh
sudo chown -R prometheus:prometheus /etc/prometheus /var/lib/prometheus
sudo chown prometheus:prometheus /usr/local/bin/prometheus
sudo chown prometheus:prometheus /usr/local/bin/promtool
```

---

# **🔹 10. Configure systemd Service**

Create the service file:

```sh
sudo nano /etc/systemd/system/prometheus.service
```

Paste this:

```
[Unit]
Description=Prometheus Monitoring
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/var/lib/prometheus \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
```

Save & exit.

---

# **🔹 11. Start and Enable Prometheus**

```sh
sudo systemctl daemon-reload
sudo systemctl start prometheus
sudo systemctl enable prometheus
sudo systemctl status prometheus
```

---

# **🔹 12. Adjust Firewall / Security Group**

Ensure your EC2 security group allows:

| Port     | Purpose           |
| -------- | ----------------- |
| **9090** | Prometheus Web UI |

---

# **🔹 13. Access Prometheus UI**

Open in browser:

```
http://<EC2_PUBLIC_IP>:9090
```

---

