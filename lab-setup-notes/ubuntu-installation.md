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
- **Network:** Bridged Adapter (for agent to connect properly)
