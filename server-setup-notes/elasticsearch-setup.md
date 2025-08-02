Installed as per instruction from the official website - https://www.elastic.co/docs/deploy-manage/deploy/self-managed/install-elasticsearch-with-debian-package
## Steps: 
### 1. Downloading GPG signing key and printing it to stdout
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
```
- `wget -qO -` downloads the Elastic GPG signing key and prints it.
- This adds the GPG public key used to verify that the downloaded packages from Elastic are legit.
### 2. Installation of Elasticsearch
> Note: There are multiple ways to install Elasticsearch (e.g., .tar.gz, Docker, APT). This guide uses the APT repository method as it's more straightforward for Ubuntu-based systems.
- as per official documentation, you may need to install the `apt-transport-https` package on Debian before proceeding, so I've run the command:
	- `sudo apt-get install apt-transport-https`
- Saved the repository definition to `/etc/apt/sources.list.d/elastic-9.x.list` via following command:
```
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/9.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-9.x.list
```
- command above allows you to install the latest versions of Elasticsearch, Logstash, and Kibana via `apt`, just like regular Debian packages.
- Installed the Elasticsearch Debian package:
```
sudo apt-get update && sudo apt-get install elasticsearch
```
### 3. Changes to config file
- config file located at `/etc/elasticsearch/elasticsearch.yml`
- uncommented and changed some fields according to the official instruction
- below are all uncommented fields and their values:
```
cluster.name: elasticsearch-test
path.data: /var/lib/elasticsearch
path.logs: /var/log/elasticsearch
network.host: 0.0.0.0
xpack.security.enabled: true
xpack.security.enrollment.enabled: true
xpack.security.http.ssl:
  enabled: true
  keystore.path: certs/http.p12
xpack.security.transport.ssl:
  enabled: true
  verification_mode: certificate
  keystore.path: certs/transport.p12
  truststore.path: certs/transport.p12
cluster.initial_master_nodes: ["mktacs-VirtualBox"]
http.host: 0.0.0.0
transport.host: 0.0.0.0
```
> `network.host: 0.0.0.0` allows Elasticsearch to listen on all network interfaces. This is fine for a lab, but insecure for production environments.
### 4. Start & enable elasticsearch
- Making sure it’s running and starts on boot:
```
sudo systemctl enable elasticsearch && sudo systemctl start elasticsearch
```
- You can check the status via: 
```
sudo systemctl status elasticsearch
```
### 5. Password and token
- Reset the superuser password via `/usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic`
  - this one is for accessing kibana web interface
- generate enrollment token for kibana via `/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana`
  - use it later to access kibana
 
---
### Summary
Elasticsearch is now installed and running with TLS and security features enabled. You’ve also generated credentials and a Kibana enrollment token for the next step.
Proceed to [`kibana-setup.md`](./kibana-setup.md) to finish the Elasatic Stack setup
