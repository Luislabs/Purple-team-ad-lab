# Purple-team-ad-lab
<div align="center">

<h1>🟧 Splunk Purple Team AD Homelab</h1>

<p>
<b>Setup Documentation • Network Topology • Log Ingestion Proof</b><br/>
Building a realistic Active Directory lab and shipping telemetry into Splunk for purple-team testing.
</p>

<p>
  <img src="https://img.shields.io/badge/Splunk-Enterprise-FF6200?style=for-the-badge&logo=splunk&logoColor=white" />
  <img src="https://img.shields.io/badge/Sysmon-Operational-111827?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Windows-Event%20Logs-0078D4?style=for-the-badge&logo=windows&logoColor=white" />
  <img src="https://img.shields.io/badge/Universal%20Forwarder-Enabled-16A34A?style=for-the-badge" />
</p>

<hr/>

</div>

<h2>✅ Current Status</h2>

<ul>
  <li><b>Topology created</b> and documented</li>
  <li><b>Sysmon installed</b> on DC + workstations</li>
  <li><b>Splunk Universal Forwarder</b> shipping logs into Splunk</li>
  <li><b>Ingestion verified</b> with Splunk searches + screenshots</li>
</ul>

<blockquote>
<b>Next:</b> detections, dashboards, and incident-style writeups (SOC workflow).
</blockquote>

<hr/>

<h2>🧱 Lab Environment</h2>

<table>
  <tr>
    <th align="left">Component</th>
    <th align="left">Purpose</th>
    <th align="left">Telemetry</th>
  </tr>
  <tr>
    <td><b>Windows Server (Domain Controller)</b><br/>AD DS + DNS</td>
    <td>Identity + authentication source of truth</td>
    <td>Sysmon + Security logs</td>
  </tr>
  <tr>
    <td><b>Windows Enterprise Workstation 1</b></td>
    <td>Endpoint activity + user behavior</td>
    <td>Sysmon + Security logs</td>
  </tr>
  <tr>
    <td><b>Windows Enterprise Workstation 2</b></td>
    <td>Second endpoint for lateral movement scenarios</td>
    <td>Sysmon + Security logs</td>
  </tr>
  <tr>
    <td><b>Ubuntu Server</b><br/>Splunk Enterprise</td>
    <td>Central log collection + search + dashboards</td>
    <td>Indexes: <code>sysmon</code> + <code>main</code></td>
  </tr>
  <tr>
    <td><b>Kali Linux</b></td>
    <td>Lab-only testing / validation</td>
    <td>N/A (optional tooling)</td>
  </tr>
</table>

<hr/>

<h2>🧩 Logging Pipeline</h2>

<p>
<b>Sysmon + Windows Event Logs</b> → <b>Splunk Universal Forwarder</b> → <b>Splunk Receiver (TCP 9997)</b> → <b>Search / Dashboards</b>
</p>

<ul>
  <li><b>Sysmon Channel:</b> <code>Microsoft-Windows-Sysmon/Operational</code></li>
  <li><b>Security Events:</b> authentication + account activity (example: 4624/4625/4672/4740)</li>
</ul>

<hr/>

<h2>🌐 Network Topology</h2>

<img width="4212" height="2392" alt="topology_neat_endpoints_oslabels_v6" src="https://github.com/user-attachments/assets/e0d4d730-e8fe-42a0-afe7-264dc0a62b7b" />


<hr/>

<h2>📸 Proof of Ingestion</h2>

<img width="2557" height="1352" alt="image" src="https://github.com/user-attachments/assets/177655ce-94ae-4962-9870-ba5119a29808" />


<details>
  <summary><b>1) Sysmon index created</b> (click to expand)</summary>
  <br/>
  <p><img src="screenshots/splunk-sysmon-index.png" width="900"/></p>
  <p><i>Shows the <code>sysmon</code> index exists and is ready for ingestion.</i></p>
</details>

<details>
  <summary><b>2) Sysmon events arriving from hosts</b> (click to expand)</summary>
  <br/>
  <p><img src="screenshots/splunk-sysmon-events.png" width="900"/></p>
  <p><i>Shows Sysmon events ingested from the DC + workstations (counts by host / EventCode).</i></p>
</details>

<details>
  <summary><b>3) Windows Security events arriving (authentication)</b> (click to expand)</summary>
  <br/>
  <p><img src="screenshots/splunk-security-events.png" width="900"/></p>
  <p><i>Shows Windows Security log ingestion (ex: success/failure logon activity).</i></p>
</details>

<hr/>

<h2>🛠️ Notes / Tuning</h2>

<ul>
  <li>Sysmon tuned to reduce noise (example: excluding Splunk Universal Forwarder binaries from ProcessCreate where appropriate).</li>
  <li>Separate indexing strategy: high-volume Sysmon data in <code>sysmon</code>, other events in <code>main</code>.</li>
</ul>

<hr/>

<h2>🚀 Roadmap</h2>

<ul>
  <li><b>Dashboard:</b> Authentication & Identity (4624/4625/4672/4740)</li>
  <li><b>Dashboard:</b> Endpoint Process & Command Line (Sysmon Event ID 1)</li>
  <li><b>Dashboard:</b> AD / DC Security (account + group changes)</li>
  <li><b>Writeups:</b> incident-style reports with timelines + Splunk searches</li>
</ul>
