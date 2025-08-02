## Steps:
### 1. Fleet server creation
- fleet creation is pretty straight forwards, although I had issues on my last attempt.
- first of all I had to create a fleet server, which must contain a name and URL
- navigate to **Fleet > Agents**, then choose **Add fleet server**
- You’ll be asked to define:
  - **Name**: Any identifier you like (e.g., `fleet-server-01`)
  - **URL**: Must be the IP address or domain of the machine hosting the Fleet Server (not `localhost` unless you're into pain)
  
<details>
<summary>Click to view screenshot</summary>
<img width="664" height="896" alt="image" src="https://github.com/user-attachments/assets/7e9688b2-5a67-4c1b-8672-954f5901441d" />
</details>
    
### 2. Agent installation
- Select the **Linux x86_64** platform when prompted.
- Kibana will generate a command to drop into cli in order to install the agent with correct token and config.
- After installation the agent will appear, status should be "Healthy", see the screenshot below:
<details>
<summary>Click to view screenshot</summary>
<img width="1322" height="726" alt="Screenshot 2025-08-02 184557" src="https://github.com/user-attachments/assets/cab2785a-f111-4d74-b8b3-7bd2a9aa98ed" />
</details>

### Notes and issues
- If the Elastic Agent appears as Offline after a reboot, make sure the Fleet config uses your machine’s local IP `192.168.x.x`, not `localhost` or `127.0.0.1`
--- 
That's it for the fleet setup. With everything set on my server I moved to [victim-machine-setup](../victim-machine-setup/)
