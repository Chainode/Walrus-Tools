# Install and Configure Grafana

### Install necessary packages and Grafana  
```
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install -y apt-transport-https software-properties-common wget
sudo mkdir -p /etc/apt/keyrings/
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
sudo apt-get update
sudo apt-get install grafana -y
```



### Start Grafana server  
```
sudo systemctl start grafana-server  
```
  
### Enable Grafana server at startup  
```
sudo systemctl enable grafana-server  
```
  
### Check the status of Grafana server 
```
sudo systemctl status grafana-server  
```
  
  
As an end result you should be able to reach your Grafana endpoint by calling it in a browser window: http://IP:3000  
By default port 3000 is used. The default user is *admin* and the initial password is also *admin*, which is strongly recommended to be changed to a much stronger password.  
Also make sure that your firewall allows you to connect to your Grafana endpoint.

In Grafana first add Prometheus as a new data source under *Configuration*. Define *"Prometheus"* as name for the data source and as URL enter "http://localhost:9091" if you are running all components (Grafana and Prometheus on the same instance). Otherwise you will have to enter the *IP* of the machine where Prometheus is running instead of *localhost* - "http://IP:9091".
