## Steps:
### 1. Kibana installation
- Since I already have correct repo and keys, simply run `sudo apt install kibana` in order to install it
### 2. Kibana configuration
- then, I had to make changes to kibana config located at `/etc/kibana/kibana.yml`
- below are all uncommented fields and their values:
```
server.host: 0.0.0.0
elasticsearch.hosts: [https://192.168.0.129:9200]
logging.appenders.file.type: file
logging.appenders.file.fileName: /var/log/kibana/kibana.log
logging.appenders.file.layout.type: json
logging.root.appenders: [default, file]
pid.file: /run/kibana/kibana.pid
elasticsearch.serviceAccountToken: <token>
elasticsearch.ssl.certificateAuthorities: [/var/lib/kibana/ca.crt]
xpack.fleet.outputs: [{id: fleet-default-output, name: default, is_default: true, is_default_monitoring: true, type: elasticsearch, hosts: [https://192.168.0.129:9200], ca_trusted_fingerprint: <fingerprint>}]
```
> Note: "hosts" field in "xpack.fleet.outputs" row must contain local ip address, not "localhost", otherwise other agents won't be able to communicate with elasticsearch thus it won't work.
> Once again, "server.host: 0.0.0.0" appropriate only for a lab environment, not the production.
### 3. Kibana start and access
- Now I can start it and try to access via the browser.
- Starting the kibana.service process and enabling it on the startup via `sudo systemctl enable kibana && sudo systemctl start kibana`
- Opened and enrolled with the token I have generated earlier in [elasticsearch-setup.md](./elasticsearch-setup.md):
- Kibana can be accessed via `localhost:5601` or `http://<machine-ip>:5601`
> Note: HTTPS won't work, make sure you are using HTTP or simply access it via localhost.
- Kibana asks to insert the enrollment token and asks for the verification code which can be generated via `sudo /usr/share/kibana/bin/kibana-verification-code`
- Then it asks for the credentials to sign in, username of superuser is "elastic", and I have generated a password earlier.
### 4. Fleet preconfigurations
- Went to "Fleet", it gave an error message "Unable to initialize Fleet. Agent binary source needs encrypted saved object api key to be set"
- generated 3 different keys via `openssl rand -base64 32`
- added 3 more fields to kibana's config file:
```
xpack.encryptedSavedObjects.encryptionKey: "generated_string"
xpack.reporting.encryptionKey: "another_generated_string"
xpack.security.encryptionKey: "yet_another_generated_string"
```
> Kibana requires these encryption keys to securely store agent policies, reporting data, and other sensitive config. Without them, Fleet initialization fails with an "Agent binary source needs encrypted saved object api key" error.
---
That's it for Kibana configuration. Proceed to [fleet-setup](./fleet-setup.md).
