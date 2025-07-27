### ElasticSearch installation process
Installed as per instruction from the official website - https://www.elastic.co/docs/deploy-manage/deploy/self-managed/install-elasticsearch-with-debian-package
#### Steps: 
##### 1. Downloading GPG signing key and printing it to stdout
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
```
- `wget -qO -` downloads the Elastic GPG signing key and prints it.
- This adds the GPG public key used to verify that the downloaded packages from Elastic are legit.
##### 2. Installation of Elasticsearch
- it can be done manually or from the apt repo, below is the second method
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
##### 3. Start & enable elasticsearch
- Making sure it’s running and starts on boot:
```
sudo systemctl enable elasticsearch | sudo systemctl start elasticsearch
```
- You can check the status via: 
```
sudo systemctl status elasticsearch
```
### Kibana installation process
- Since we already have correct repo and keys, simply run `sudo apt install kibana` in order to install it
- then, just as in case with elasticsearch I enabled it for startup and started it
```
sudo systemctl enable kibana
sudo systemctl start kibana
```
- afterwards I changed the configuration file just to test whether kibana is accessible
- the configuration file's path is `/etc/kibana/kibana.yml`
- Had to uncomment just 2 fields for now
	- `server.host: "0.0.0.0"`
	- `elasticsearch.hosts: ["http://localhost:9200"]`
- then restarted kibana with `sudo systemctl restart kibana` and that's it, it is working now >
<img width="2258" height="1105" alt="Screenshot 2025-07-27 033144" src="https://github.com/user-attachments/assets/d470d597-65f6-4202-b9d1-d938e93c2267" />
- token generation is straight-forward, there is a button "Where do I find this?" which explains what command to run
- then another command to get the verification code and then sign in menu shows up, where I had to put username and password (user elastic exists by default, password was generated when I just installed the elasticsearch
### Logstash installation process
- For now I just installed it on the server machine with `sudo apt install logstash`
- Will continue tomorrow
