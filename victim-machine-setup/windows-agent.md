## Steps:
### 1. Agent installation.
- On the **Fleet > Agents** page, select **"Add Agent"**
- Create an agent policy
  - I turned off the metrics from the policy cause I don't really need them.
  - By default it only has "System" integration, I will add more integrations later on.
- Select **Enroll in Fleet**
- Select **Windows x86_64**
- Kibana will generate a PowerShell command, copy and run it in PowerShell opened as Administrator.
> Note: you should add `--insecure` after the token since self-signed certs are being used.
### 2. Verifying Installation
- Open Kibana > Fleet > Agents
- The Windows machine should appear within ~30 seconds, marked Healthy
<details> <summary> Click to view screenshot </summary>
<img width="1326" height="629" alt="image" src="https://github.com/user-attachments/assets/b0cefd69-6073-4c85-8cc6-19bbd96ff571" /> </details>

- You can also verify that the logs are ingesting into Kibana on "Discover" page:

<details> <summary> Click to view screenshot </summary>
<img width="1317" height="935" alt="image" src="https://github.com/user-attachments/assets/c29a803f-5ec9-4957-9a91-2159157c9ff5" /> </details>
- And after a fresh installation I had to verify that this time Application/Security/System logs are being shipped
- Created an Application logs source via:

```
New-EventLog -LogName Application -Source "TestSource"
```

- Generated a test log via: 

```
Write-EventLog -LogName Application -Source "TestSource" -EntryType Information -EventId 1000 -Message "Hello from test log!"
```

- It went through, see the screenshot below:
<details> <summary> Click to view screenshot </summary>
<img width="1124" height="535" alt="Screenshot 2025-08-03 232114" src="https://github.com/user-attachments/assets/d560005e-9fc7-4d31-b098-69ec96a9409b" />
</details>

---

- After verifying the agent is up and running we can proceed with [sysmon-setup.md](./sysmon-setup.md)
