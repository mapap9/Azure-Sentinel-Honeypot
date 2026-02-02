<h1>Azure Sentinel Honeypot</h1>

<h2>Description</h2>
Project consists of a walkthrough for a honeypot deployed on Azure with Sentinel and Log Analytics.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Sentinel</b> 
- <b>KQL</b> 

<h2>Environments Used </h2>

- <b>Windows 10</b> (22H2)
- <b>Microsoft Azure</b> (22H2)

<h2>Walk-through:</h2>

<p align="center">
<h2>1.	Create the Resource Group </h2><br/>
<img src="images/1.png" height="80%" width="80%" alt=""/>
<br />
<b>You need an active Azure subscription. After subscribing, create a resource group in your preferred region and give it a distinctive name for easy identification — for example: RG-SOC-Lab. </b>
<br />
<br />
  
<h2>2.	Create the Virtual Network  </h2><br/>
<img src="images/2.png" height="80%" width="80%" alt=""/>
<img src="images/3.png" height="80%" width="80%" alt=""/>
<img src="images/4.png" height="80%" width="80%" alt=""/>
<br />
<b>The Resource Group and Virtual Machine must be internet-connected. First, set up a virtual network to create the subnet the VM will reside on. Use the default settings and name the virtual network VNet-SOC-Lab. </b>
<br />
<br />
  
<h2>3.	Create the Virtual Machine </h2><br/>
<img src="images/5.png" height="80%" width="80%" alt=""/>
<img src="images/6.png" height="80%" width="80%" alt=""/>
<img src="images/7.png" height="80%" width="80%" alt=""/>
<img src="images/8.png" height="80%" width="80%" alt=""/>
<img src="images/9.png" height="80%" width="80%" alt=""/>
<br />
<b>Create a Windows 10 Enterprise virtual machine and assign it an inconspicuous name (for example, CORP-NET-AU-1) so it doesn't appear to be a honeypot. After exposing the VM to the internet it may receive connections quickly—often within minutes. Provide a simple username and password and ensure the VM is deployed to the same virtual network you created earlier.  </b>
<br />
<br />
  
<h2>4.	Expose VM to the Internet  </h2><br/>
<img src="images/10.png" height="80%" width="80%" alt=""/>
<img src="images/11.png" height="80%" width="80%" alt=""/>
<img src="images/12.png" height="80%" width="80%" alt=""/>
<br />
<b>Create an inbound rule that exposes the VM to the internet by replacing the default rules with a permissive custom rule that allows all traffic. This is intentionally unsafe and should never be used in production; it’s for a honeypot environment only. Name the rule DANGER_AllowAnyCustomAnyInbound.  </b>
<br />
<br />
  
<h2>5.	Remote into VM and Disable Firewall  </h2><br/>
<img src="images/13.png" height="80%" width="80%" alt=""/>
<img src="images/14.png" height="80%" width="80%" alt=""/>
<img src="images/15.png" height="80%" width="80%" alt=""/>
<br />
<b>Obtain the VM's public IP and RDP into it using the credentials you created. Once connected, disable the firewall completely to leave the machine exposed to all incoming traffic. </b>
<br />
<br />

<h2>6.	Creating the Log Analytics Workspace </h2><br/>
<img src="images/16.png" height="80%" width="80%" alt=""/>
<br />
<b>Create a Log Analytics workspace and connect it to the VM so it forwards events. Name the workspace LAW-SOC-Lab-0000 for easy identification.  </b>
<br />
<br />
  
<h2>7.	Linking Microsoft Sentinel </h2><br/>
<img src="images/17.png" height="80%" width="80%" alt=""/>
<img src="images/18.png" height="80%" width="80%" alt=""/>
<br />
<b>Proceed to link Microsoft Sentinel to the Log Analytics Workspace.  </b>
<br />
<br />

<h2>8.	Connect VM to Log Analytics Workspace </h2><br/>
<img src="images/19.png" height="80%" width="80%" alt=""/>
<img src="images/20.png" height="80%" width="80%" alt=""/>
<img src="images/21.png" height="80%" width="80%" alt=""/>
<img src="images/22.png" height="80%" width="80%" alt=""/>
<img src="images/23.png" height="80%" width="80%" alt=""/>
<img src="images/24.png" height="80%" width="80%" alt=""/>
<img src="images/25.png" height="80%" width="80%" alt=""/>
<img src="images/26.png" height="80%" width="80%" alt=""/>
<img src="images/27.png" height="80%" width="80%" alt=""/>
<img src="images/28.png" height="80%" width="80%" alt=""/>
<br />
<b>Connect the VM to the Log Analytics workspace (Sentinel enabled). In Microsoft Sentinel, install the Windows Security Events solution to simplify event parsing. Configure Windows Security Events using the Azure Monitor Agent (the legacy method is deprecated). Create a Security Event data collection rule, link it to the Windows VM, and verify the agent/extension appears on the VM.   </b>
<br />
<br />

<h2>9.	Querying with KQL </h2><br/>
<img src="images/29.png" height="80%" width="80%" alt=""/>
<img src="images/30.png" height="80%" width="80%" alt=""/>
<br />
<b>Start with basic KQL queries such as "SecurityEvents". Initial results show routine activity with no clear signs of compromise. However, after about five minutes—while creating the watchlist—suspicious activity began appearing, indicating probing attempts.   </b>
<br />
<br />

<h2>10.	Creating the Watchlist </h2><br/>
<img src="images/31.png" height="80%" width="80%" alt=""/>
<img src="images/32.png" height="80%" width="80%" alt=""/>
<img src="images/33.png" height="80%" width="80%" alt=""/>
<img src="images/34.png" height="80%" width="80%" alt=""/>
<img src="images/35.png" height="80%" width="80%" alt=""/>
<br />
<b>Create a watchlist in Microsoft Sentinel and upload a database file of locations and IPs (for example, MaxMind's GeoIP database). In production, this data would typically come from your provider's backend.   </b>
<br />
<br />

<h2>11.	Creating the Threat Map </h2><br/>
<img src="" height="80%" width="80%" alt=""/>
<img src="images/36.png" height="80%" width="80%" alt=""/>
<img src="images/37.png" height="80%" width="80%" alt=""/>
<img src="images/38.png" height="80%" width="80%" alt=""/>
<img src="images/39.png" height="80%" width="80%" alt=""/>
<img src="images/40.png" height="80%" width="80%" alt=""/>
<img src="images/41.png" height="80%" width="80%" alt=""/>
<img src="images/42.png" height="80%" width="80%" alt=""/>
<img src="images/43.png" height="80%" width="80%" alt=""/>
<img src="images/44.png" height="80%" width="80%" alt=""/>
<img src="images/45.png" height="80%" width="80%" alt=""/>
<img src="images/46.png" height="80%" width="80%" alt=""/>
<br />
<b>Create a threat map using Workbooks that references the watchlist you imported (network/location data). Build an interactive map showing attacking locations and relevant metrics, save the workbook, and revisit the underlying query anytime. For example, you might see large volumes—e.g., 22,000 events from a single IP range (And this was only within 4 hours!) —with location mismatches (Argentina vs. some connections from Ukraine), suggesting proxying or botnet activity.   </b>
<br />
<br />
<b>Here we can input queries such as: 
"let GeoIPDB_FULL = _GetWatchlist("geoip");
SecurityEvent
| where EventID == 4625
| where IpAddress == "IP HERE"
| evaluate ipv4_lookup(GeoIPDB_FULL, IpAddress, network)
| order by TimeGenerated desc
"
</b>
<br />
<br />
<b>This query will target Security Events, specifically, failed logons using the watchlist we created before. You must input an attacker IP from one of the previous queries. It will correlate attacking ip's with locational data. </b>
<br />
<br />

</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
