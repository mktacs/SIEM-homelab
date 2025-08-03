## Steps:
### 1. Fleet server creation
- luckily I didn't need to manually install 8.18 version of elastic agent, kibana automatically suggests this version is required.
- first of all I had to create a fleet server, which must contain a name and URL
- navigate to **Fleet > Agents**, then choose **Add fleet server**
- First of all new policy creation required.
  - For the fleet server I disabled both logs and metrics, cause I don't need any logs from the server itself in my case
  - So I've unchecked "Collect system logs and metrics" and "Collect agent logs", "Collect agent metrics" in advanced settings, see the screenshots below:
<details>
<summary>Click to view screenshots</summary>
<img width="474" height="816" alt="Screenshot 2025-08-03 230954" src="https://github.com/user-attachments/assets/b9b5cdb7-a07e-4483-bd19-c7ca123566ca" />
<img width="472" height="813" alt="Screenshot 2025-08-03 230949" src="https://github.com/user-attachments/assets/86c25125-da1e-4890-b8c6-9b525bcf0351" />
</details>

- Then I defined fleet name and URL:
  - **Name**: Any identifier you like (e.g., `fleet-server-01`)
  - **URL**: Must be the IP address or domain of the machine hosting the Fleet Server (not `localhost` unless you're into pain)
<details>
<summary>Click to view screenshot</summary>
<img width="472" height="819" alt="Screenshot 2025-08-03 231144" src="https://github.com/user-attachments/assets/1eda91cb-bd18-47fa-89c3-8b25de5c717d" />
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
