installed as per official instruction: [link](https://www.elastic.co/guide/en/elasticsearch/reference/8.18/deb.html)
## Steps:
### 1. Downloaded and installed GPG keys
- Command below:
`wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg`
### 2. Installing the ElasticSearch via apt repository
- You may need to install the apt-transport-https package on Debian before proceeding:
  - `sudo apt-get install apt-transport-https`
- Save the repository definition to /etc/apt/sources.list.d/elastic-8.x.list:
  - `echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list`
- Verified the available versions via:
  - `apt list -a elasticsearch`
- As per bug report that I encountered, 8.18.0 is working fine so I proceeded with this version:
  - `sudo apt-get install elasticsearch=8.18.0`
- Locked the version via:
  - `sudo apt-mark hold elasticsearch`
### 3. elasticsearch.yml configuration
- configured it just as the previous time, here is the all uncommented fields:
```yml
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
cluster.initial_master_nodes: ["mktacs"]
http.host: 0.0.0.0
transport.host: 0.0.0.0
```
> P.S: the yml file located at /etc/elasticsearch/
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
- Reset the superuser password via:
```
sudo /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
```
> this one is for accessing kibana web interface

- generate enrollment token for kibana via:
```
sudo /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
```
> use it later to access kibana
---
### Summary
Elasticsearch is now installed and running with TLS and security features enabled. I've also generated credentials and a Kibana enrollment token for the next step.
Proceed to [kibana-8.18-setup.md](./kibana-8.18-setup.md)
