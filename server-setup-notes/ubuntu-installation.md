# Ubuntu installation and Preparations
This machine will act as a server with elasticsearch, kibana, it will also act as a fleet server.
---
## 1. Ubuntu version & Download
- **Version used:** Ubuntu Desktop 24.04.2 LTS
- **Download link:** https://ubuntu.com/download/desktop
- **Install method:** Virtual Machine via VirtualBox
> Note: I used Ubuntu Desktop instead of the Server edition to simplify navigation and avoid confusion while testing Elastic Stack components. This increased resource usage but provided easier GUI access to tools and browser-based services like Kibana.
## 2. VM Configuration
- **RAM:** 24GB (started with 16, it was pretty sluggish after installation of elasticsearch & kibana, increased to 24)
- **CPU:** 8 cores
- **Disk:** 50GB dynamically allocated
## 3. Network setup
- Set Network Adapter to Bridged mode.
- Changed netplan config, basically disabled dhcp so the local IP won't change:
```
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.0.129/24]
      routes:
        - to: 0.0.0.0/0
          via: 192.168.0.1
      nameservers:
        addresses: [8.8.8.8,8.8.4.4]
```
---
That's it for the machine itself. Proceed to [`elasticsearch-setup.md`](./elasticsearch-setup.md)
