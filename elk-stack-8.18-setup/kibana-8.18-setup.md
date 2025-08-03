## Steps:
### 1. Kibana 8.18.0 installation via apt repository
- Installing same version as elasticsearch, command below:
```
sudo apt-get install kibana=8.18.0
```
> Note: it is important that kibana and elasticsearch have the same version
- locking the version via:
```
sudo apt-mark hold kibana
```
### 2. Kibana configuration
- Had to uncomment and change only the `server.host` and `elasticsearch.host` fields
- all uncommented fields below:
```yml
server.host: 0.0.0.0
elasticsearch.hosts: [http://localhost:9200]
logging.appenders.file.type: file
logging.appenders.file.fileName: /var/log/kibana/kibana.log
logging.appenders.file.layout.type: json
logging.root.appenders: [default, file]
pid.file: /run/kibana/kibana.pid
```
> Note: `server.host: 0.0.0.0` field makes kibana listen on all network interfaces. It's okay for lab environment but overall - not safe
> Note#2: this is the initial config, once you will enroll and sign in, kibana.yml config will be slightly changed automatically, including `elasticsearch.hosts: ['https://192.168.0.129:9200']` field
### 3. Kibana start and access
- Now I can start it and try to access via the browser.
- Starting the kibana.service process and enabling it on the startup via `sudo systemctl enable kibana && sudo systemctl start kibana`
- Opened and enrolled with the token I have generated earlier in [elasticsearch-setup.md](./elasticsearch-setup.md):
- Kibana can be accessed via `localhost:5601` or `http://<machine-ip>:5601`
  - since I am opening it outside of VM, im using `http://<machine-ip>:5601`
> Note: HTTPS won't work, make sure you are using HTTP or simply access it via localhost.
- Kibana asks to insert the enrollment token and asks for the verification code which can be generated via `sudo /usr/share/kibana/bin/kibana-verification-code`
- Then it asks for the credentials to sign in, username of superuser is "elastic", and I have generated a password earlier.
