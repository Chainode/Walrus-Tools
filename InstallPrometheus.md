# Prometheus Installation and Configuration  

### Verify available versions
```
sudo apt-cache policy prometheus  
```

### Create Prometheus user  
```
sudo useradd -M -r -s /bin/false prometheus  
```

### Create Prometheus directories  
```
sudo mkdir /etc/prometheus /var/lib/prometheus  
```

### Download binaries  
```
wget https://github.com/prometheus/prometheus/releases/download/v3.1.0/prometheus-3.1.0.linux-amd64.tar.gz  
```

### Extract and Install  
```
tar xzf prometheus-3.1.0.linux-amd64.tar.gz  
sudo cp prometheus-3.1.0.linux-amd64/{prometheus,promtool} /usr/local/bin/  
sudo chown prometheus:prometheus /usr/local/bin/{prometheus,promtool} 
```


### Setup Prometheus configuration  
```
sudo cp prometheus-3.1.0.linux-amd64/prometheus.yml /etc/prometheus/prometheus.yml  
sudo nano /etc/prometheus/prometheus.yml  
```

### Configuration section for scraping  
```
    static_configs:  
    - targets: ['localhost:9091']  
  
  - job_name: 'Walrus-Node'  
    static_configs:  
      - targets: ['localhost:9184']  
        labels:  
          group: 'WalrusNode'  

  - job_name: 'Walrus-Aggregator'
    static_configs:
      - targets: ['localhost:27182']
        labels:
          group: 'WalrusAggregator'

  - job_name: 'Walrus-Publisher'
    static_configs:
      - targets: ['localhost:27183']
        labels:
          group: 'WalrusPublisher'

  - job_name: node  
    static_configs:  
      - targets: ['localhost:9100']  

```

The ports 9184, 27182, 27183 for the Walrus Storage Node, Walrus Publisher and Walrus Aggregator are just examples and have to be changed accordingly to the ports your services are exposing metrics. 
The same applies to the node or Prometheus port or host ("localhost") — they can be adapted as needed.
        
### Set the user and group ownership on the configuration file
```
sudo chown -R prometheus:prometheus /etc/prometheus  
sudo chown prometheus:prometheus /var/lib/prometheus  
```
  
### Create a systemd file for Prometheus - in this scenario Prometheus uses 9091 as listen port
```
sudo nano /etc/systemd/system/prometheus.service  
```
Now copy the section below:  
```
[Unit]  
Description=Prometheus Time Series Collection and Processing Server  
Wants=network-online.target  
After=network-online.target  
  
[Service]  
User=prometheus  
Group=prometheus  
Type=simple  
ExecStart=/usr/local/bin/prometheus \  
    --config.file /etc/prometheus/prometheus.yml \  
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.listen-address="0.0.0.0:9091"  
  
[Install]  
WantedBy=multi-user.target  
```
  
### Enable Prometheus at startup  
```
sudo systemctl enable prometheus  
```
### Start Prometheus service  
```
sudo systemctl start prometheus  
```
### Check the status of the Prometheus service  
```
sudo systemctl status prometheus  
```
