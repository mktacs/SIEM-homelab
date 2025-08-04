## Steps:
### 1. Downloaded ISO file from [official website](https://ubuntu.com/download/server/thank-you?version=24.04.2&architecture=amd64&lts=true)
### 2. Installed on Virtual Box
  - Selected OpenSSH installation in the process
### 3. Changed Network Adapter to bridged in VBox settings.
  - Required to successfull fleet setup, etc.
### 4. Changed the netplan config to:
```
network:
  version: 2
  renderer: networkd
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
### 5. Connected to VM via SSH via `ssh <username>@ip`
---
That's all for the initial VM setup, proceed to [elasticsearch-8.18-setup.md](./eleasticsearch-8.18-setup.md)
