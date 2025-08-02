## Steps:
### 1. Agent installation.
- On the **Fleet > Agents** page, select **"Add Agent"**
- Create an agent policy
  - I didn't change any policy's configs.
  - By default it only has "System" integration, I will add more integrations later on.
- Select **Enroll in Fleet**
- Select **Windows x86_64**
- Kibana will generate a PowerShell command, copy and run it in PowerShell opened as Administrator.
> Note: it may run into some certificate problems, add `--insecure` after the token in order to workaround it.
### 2. Verifying Installation
- Open Kibana > Fleet > Agents
- The Windows machine should appear within ~30 seconds, marked Healthy
<details> <summary> Click to view screenshot </summary>
<img width="1326" height="629" alt="image" src="https://github.com/user-attachments/assets/b0cefd69-6073-4c85-8cc6-19bbd96ff571" /> </details>

- You can also verify that the logs are ingesting into Kibana on "Discover" page:

<details> <summary> Click to view screenshot </summary>
<img width="1317" height="935" alt="image" src="https://github.com/user-attachments/assets/c29a803f-5ec9-4957-9a91-2159157c9ff5" /> </details>

---

- After verifying out agent is up and running we can go configure the [integrations-setup.md](./integrations-setup.md)
