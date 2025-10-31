<br><h1 align="center">Networking: DNS Servers, Caches, and CNAMEs</br>
<br>
<img src="https://www.sectorlink.com/img/blog/dns-servers.png" alt="isaiahmurphy" height="300" width="300"/></br>
</h1>
In this lab, we'll be testing the fetching process of DNS caches through a virtual Windows OS.
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
Create a resource group within Azure. This will be used to store both virtual machines once they're created.
<br><img src="https://github.com/user-attachments/assets/a8f2c340-ec7a-4168-a111-8d9148e19f78" height="75%" width="100%" alt="Disk Sanitization Steps"/>
<br/>
</p>
