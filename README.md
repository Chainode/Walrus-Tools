# Walrus-Tools

## Monitoring Walrus Storage Node, Publisher, Aggregator as well as the underlying Hardware, using Grafana & Prometheus


## Scope

With this solution it will be possible to monitor your Walrus Storage Node, Publisher, Aggregator and the underlying hardware. This will help you improve the overall health of your Walrus stack as well as offer you proper insight into what happens with your machine at any point in time.  
Prometheus represents a monitoring solution for storing time series data like metrics. Grafana is another important complementary tool which allows users to visualize the data stored in Prometheus and many more sources like Telegraf, etc.  

In combination with an Alertmanager it becomes a viable solution to monitor and improve the overall uptime and performance of your Walrus stack. Alertmanager can be used to define certain thresholds for which you will get alerted on Telegram, Discord, by SMS or many other mediums. Some example for possbile alerts: You can set your threshold for disk usage rate to 70% so that you will get alerted once that is reached in order to prepare for an upgrade for more disk space; node and epoch status; checkpoint download rate and progress; persisted, processed and pending events; and much more.  

## Prerequisites
* Enable export of Walrus metrics by specifying a valid metrics address for each of the services you want to monitor
* Node Exporter  --> please check this guide in this repo: https://github.com/Chainode/Walrus-Tools/blob/main/InstallNodeExporter.md
* Prometheus  --> please check this guide in this repo: https://github.com/Chainode/Walrus-Tools/blob/main/InstallPrometheus.md
* Grafana  --> please check this guide in this repo: https://github.com/Chainode/Walrus-Tools/blob/main/InstallGrafana.md

## Import Walrus Dashboard into Grafana  
For this you will have to download the Walrus-Dashboard.json from this repo and then in Grafana go to *Dashboards* -> *New* -> *Import* -> *Upload JSON file* and select the Walrus-Dashboard.json to be uploaded.  
During the import, the Walrus-Dashboard.json Grafana dashboard will automatically search for Prometheus datasources that contain "Walrus", "walrus" or "wal" in their name.  
This can be changed once the dashboard was imported by going to "Dashboard Settings" -> "Variables" -> "datasource" variable -> here you will see a parameter "Instance name filter" where the regex condition for selecting the Prometheus source was defined.
As a next step you should make sure the right Prometheus connection has been selected and if necessary adapt the Dashboard. 

## Final Result 
![image](https://github.com/user-attachments/assets/e315d099-fb56-43ba-b0f7-88c0fb2b3e2a)
![image](https://github.com/user-attachments/assets/3372d4c8-66f9-4e66-8f15-8bd80f7837c9)
![image](https://github.com/user-attachments/assets/5040168b-788a-4530-8a63-7ace57608402)
![image](https://github.com/user-attachments/assets/9e83a051-fda5-4824-bd6e-293c3835a50b)
![image](https://github.com/user-attachments/assets/8c3716df-404d-4970-a70c-0ee9433d4c88)
![image](https://github.com/user-attachments/assets/db8bd6d3-9966-4ae9-80cf-dd801448ae62)
