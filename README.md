<br><h1 align="center">Networking: DNS Servers, Caches, and CNAMEs</br>
<br>
<img src="https://www.sectorlink.com/img/blog/dns-servers.png" alt="isaiahmurphy" height="300" width="300"/></br>
</h1>
We'll be testing the DNS resolution process through a virtual Windows OS. This OS will be communicating with a separate, preconfigured Windows Server VM which contains a domain we can access through its Active Directory and primarily DNS Manager for this experiment. When a mapping is requested from a host, the host first checks for the domain mapping in its DNS cache, being that it's the fastest method to retrieve it. Then, it checks in its local hosts file (this is the second fastest way). And finally, it checks its local DNS server. For this test, we'll use a new host within the Windows Server domain, assign it an ip address (which we will change again later), and use a variety of networking commands to fetch and observe results from our virtual Windows OS. Understanding the resolution process will help to identify where queries could fail, and allow you to utilize networking commands to troubleshoot and potentially resolve them.
<br/>


<h2>Databases & Programs Used</h2>
<p>
 
- <b>Powershell</b>

- <b>Command Prompt</b>

- <b>DNS Managery</b>

</p>

<h2>Environments Used </h2>
<p>
 
- <b>Windows 10 Enterprise</b> (22H2)
- <b>Windows Server Datacenter: Azure Edition</b> (2022)

</p>

<h2>Step-by-Step Overview</h2>
<p>
 
- <b>Create dedicated resource group within Azure</b>

- <b>Configure and deploy virtual domain server client</b>

- <b>Configure and deploy virtual Windows 10 client</b>

- <b>Link both VMs to the same virtual network</b>

- <b>Change the domain server VM private IP address allocation to static</b>

- <b>Change the virtual Windows 10 client's DNS server to "custom" and set it to the domain server's static private IP address</b>

- <b>Install Active Directory Domain Service through the domain server client's Server Manager</b>

- <b>Promote the domain server to a domain controller</b>

- <b>Create a new forest domain (Restart Windows 10 VM)</b>

- <b>Add Windows 10 client to the domain controller's newly created Active Directory</b>

- <b>Return to the domain server client to observe and confirm the Windows 10 client exists within the Active Directory</b>

<h2>Creating Resources</h2>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/cc36cccf-2a10-4ea4-9eeb-a97fb829aec5" height="75%" width="100%"/>
<br/>
</p>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

</p>
We're first starting out within the Windows client OS. Here, I ran ping mainframe to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

Outdated DNS caches are a common network connectivity roadblock in real-world IT scenarios. Using both your knowledge of the DNS resolution process and OS networking commands, you have the tools to be able to figure out many common networking issues end-users face.
