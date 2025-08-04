## Steps:
### 1. Downloading the Sysmon and config
- It can be downloaded from the [here](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
- Created a "Sysmon" folder in the `C:\Windows\System32`
- Unarchived everything to this folder
- Downloaded config frim [SwiftOnSecurity/sysmon-config](https://github.com/SwiftOnSecurity/sysmon-config) repo, saved it to the same Sysmon folder
  - This is a well known config, although it looks like no updates were made for the last 4 years.
  - I will proceed with it for now anyway, I think it should be enough for my lab purposes, or I can update it to some other config later on.
 ### 2. Sysmon installation
- now we can install the service
  - run CMD as administrator
  - `cd` into Sysmon folder
  - command below used to run & enable the service with config:
```
sysmon.exe -accepteula -i sysmonconfig-export.xml
```
- Sysmon started, all good

<details> <summary> Click to view screenshot </summary>
<img width="736" height="374" alt="image" src="https://github.com/user-attachments/assets/2f84669f-53f7-4929-94e0-b54bb5f0064f" />
</details>

- We can double check it in the Event Viewer > Applications and Services logs > Microsoft > Windows > Sysmon > Operational
- It generates events, everything is okay

<details> <summary> Click to view screenshot </summary>
<img width="612" height="535" alt="image" src="https://github.com/user-attachments/assets/a7795d31-d2be-43ce-92a3-769ac2710283" />
</details>

### 3. "Windows" integration install
- Now we need to send the sysmon logs to the ELK
- There is integration called "Windows", it includes Sysmon logs
- So, headed to Kibana > Fleet > Agent policies > selected policy created for victim VM > Add integration > Windows
- I only disabled the metrics and name, everything else left as is, see screenshots below:
<details> <summary> Click to view screenshots </summary>
<img width="952" height="1089" alt="Screenshot 2025-08-04 134936" src="https://github.com/user-attachments/assets/88e7f668-0d90-4b2f-8272-7b33e786579a" />
<img width="843" height="1111" alt="Screenshot 2025-08-04 134945" src="https://github.com/user-attachments/assets/0d75b71b-b239-4d1f-8972-74c3b921236f" />
</details>

- Now we test if it's actually working/shipping logs
- Went to discovery and searched for `data_stream.dataset` - it shows all data streams, and now it has sysmon, powershell logs, see the screenshots below:

<details> <summary> Click to view screenshots </summary>
<img width="593" height="527" alt="Screenshot 2025-08-04 140020" src="https://github.com/user-attachments/assets/9183dff9-20e2-4d41-8bcf-7c2ff9e931c9" />
<img width="2007" height="1140" alt="Screenshot 2025-08-04 140120" src="https://github.com/user-attachments/assets/a63f7e84-65c5-4e64-89d0-46d6cf193ef3" />
</details>

> Note: there was some error message at first, I had to restart the Windows VM in order to get it to work

---
That's it for the Sysmon setup
