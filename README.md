# grafana-server
Grafana Server
```
// installation of grafana server 

t3.medium | SG-Inbound-3000

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
