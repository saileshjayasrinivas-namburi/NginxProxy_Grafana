
# Access Multiple Environments' Grafana (Private Network) via NGINX Proxy with Whitelisting

This repository contains configurations and instructions for setting up NGINX Proxy to Access Grafana Which is Hosted In private Network.

 

## Grafana Subpath configuration 

Edit CM map to add Below key values:

```
server:
  root_url = "https://your-grafana-DNS/<random name>"
  serve_from_sub_path = true

```

#### Retrieve the Grafana Namespace & use it for Below Commands 

  ``` 
kubectl get cm -n <Grafana-namespace>
kubectl edit cm <grafana-cm> -n <Grafana-namespace>

  ``` 
### After Updating Delete Running pod to update pod with new Configurations.

```
Kubectl delete pod <podname> -n <namespace>
```

#### Nginx Configuration 

# Create a Ubuntu Machine in any Private Network & run below commands to Install Nginx/Conform up and Running 

  ``` 
sudo apt-get update
sudo apt-get install nginx
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
  ``` 
  
# update Configurations Refer Nginx.conf in Repo:

#### Update nginx.conf file refer Nginx.conf in the Repo & Modify values in the keys proxy_pass, proxy_set_header Host, and proxy_set_header Origin , ssl_certificate ,ssl_certificate_key, server_name as IP or localhost, listen https values changes based on the environment & For each environment, add location section in nginx.conf file .

 
  ```
cd /etc/nginx
nano ngnix.conf  # Update Configurations in this file 
sudo systemctl restart nginx
  ``` 

## Whitelist UR IP to NGNIX machine & Update Nginx machine IP to Grafana Security Groups with HTTPS 

#### Hit the machine's IP/subpath to access Grafana. If you want to use a friendly username, map the machine's IP to a DNS. 

Use a Python script and host it to enable an endpoint that whitelists our machine's IP address when a specific URL is accessed.