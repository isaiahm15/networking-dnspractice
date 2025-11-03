<br><h1 align="center">Networking: CNAMEs, DNS Servers & Caches</br>
<br>
<img src="https://www.sectorlink.com/img/blog/dns-servers.png" alt="isaiahmurphy" height="300" width="300"/></br>
</h1>
We'll be testing the DNS resolution process through a virtual Windows OS. This OS will be communicating with a separate, preconfigured Windows Server VM which contains a forestdomain we can access through its Active Directory and primarily DNS Manager for this experiment. When a mapping is requested from a host, the host first checks for the domain mapping in its DNS cache, being that it's the fastest method to retrieve it. Then, it checks in its local hosts file (this is the second fastest way). And finally, it checks its local DNS server. For this test, we'll use a new host within the Windows Server domain, assign it an ip address (which we will change again later), and use a variety of networking commands to fetch and observe results from our virtual Windows OS. Understanding the resolution process will help to identify where queries could fail, and allow you to utilize networking commands to troubleshoot and potentially resolve them.
<br/>


<h2>Databases & Programs Used</h2>
<p>
 
- <b>Powershell</b>

- <b>Command Prompt</b>

- <b>DNS Manager</b>

</p>

<h2>Environments Used </h2>
<p>
 
- <b>Windows 10 Enterprise</b> (22H2)
- <b>Windows Server Datacenter: Azure Edition</b> (2022)

</p>

<h2>Step-by-Step Overview</h2>
<p>
 
- <b>Create new host with valid IP address in DNS Manager</b>

- <b>Ping host from Windows 10 client to allow it to store domain mapping in DNS cache</b>

- <b>Change host IP address in DNS Manager</b>

- <b>Observe that Windows 10 client network still uses old DNS mapping</b>

- <b>Clear Windows 10 client's DNS cache</b>

- <b>Ping host again to observe that the client now uses updated DNS mapping</b>

- <b>Create new Alias (CNAME) in DNS Manager and point it to a domain name of choice</b>

- <b>Ping and/or lookup alias from Windows 10 client to observe CNAME functionality</b>

</p>

<h2 align="center">Altering a domain's original DNS mapping</h2>

<p>We're first starting out within the Windows client OS. Here, I ran "<strong>ping</strong> mainframe" to confirm there is no domain created with this name yet- so next up is where we'll use this name to create a new host within our Window Server domain.
<br><img src="https://github.com/user-attachments/assets/a0765680-752f-4647-8e95-ffbf361d5227" height="75%" width="100%"/>
<br/>
</p>

</p>
Launch the DNS Manager within your Windows Server client and add a new host under your forest domain. Here we'll use the name we tried to ping for in command prompt earlier ("mainframe"). You can choose a valid IP address or use the private IP address of your Windows Server VM like I did here. Once this is set, pinging "mainframe" on the Windows OS client should populate network traffic in response from the Windows Server client.
<br><img src="https://github.com/user-attachments/assets/cc36cccf-2a10-4ea4-9eeb-a97fb829aec5" height="75%" width="100%"/>
<br/>
</p>

</p>
Returning the Windows 10 client in command prompt, we'll try running ping mainframe again. Here you can see that we get successful reply traffic from 10.0.0.4, which is our Windows Server client.
<br><img src="https://github.com/user-attachments/assets/68271ec7-193b-4830-abcd-42a09aa3acb5" height="75%" width="100%"/>
<br/>
</p>

</p>
Launch DNS Manager again (Windows Server), open the properties to your domain, and change the IP address to another valid one. I decided to change the IP from 10.0.0.4 > 8.8.8.8
<br><img src="https://github.com/user-attachments/assets/a3ba983f-c90a-4b0b-a91c-f62f695bbb6a" height="75%" width="100%"/>
<br/>
</p>

</p>
Pinging our domain again from the Windows 10 client, you'll now notice that the IP address is still 10.0.0.4. This is because the Windows 10 client already has the "mainframe" domain mapped to 10.0.0.4 in its local DNS cache.
<br><img src="https://github.com/user-attachments/assets/77c5bc19-f781-44ab-9ecf-edcaf89728e7" height="75%" width="100%"/>
<br/>
</p>

</p>
Running <strong>ipconfig /flushdns</strong> (command prompt) on the Windows 10 client will clear any existing domain mappings in its DNS cache.
<br><img src="https://github.com/user-attachments/assets/25f01323-5f02-4998-8f22-bcb6093c4d40" height="75%" width="100%"/>
<br/>
</p>

</p>
Lastly, ping your domain again from the Windows 10 client to observe changes. Now that its DNS cache is clear, the host has no mapping record of "mainframe" and has to request it from the network, which will update the mapping from 10.0.0.4 > 8.8.8.8
<br><img src="https://github.com/user-attachments/assets/225c46a2-de41-48b6-8c58-da2a69325695" height="75%" width="100%"/>
<br/>
</p>

<h2 align="center">CNAME Exercise</h2>

</p>
Next we're doing a quick exercise to understanding CNAMEs. Choose a new domain name and try pinging it from your Windows 10 client (it should result it no host being found, since we haven't created it in DNS Manager yet).
<br><img src="https://github.com/user-attachments/assets/214820ce-6bd2-4b71-a853-45f979663d6f" height="75%" width="100%"/>
<br/>
</p>

</p>
Launch DNS Manager and create an Alias (CNAME) in your forest domain. The "Alias name" field is where you'll input the domain name you pinged for in the prior step. Then, in the "Fully qualified domain anme name for target host" field you can enter a random website. I went with a popular one for example, "www.google.com"
<br><img src="https://github.com/user-attachments/assets/d6150907-3708-4b1d-a357-ecd262e1c0f3" height="75%" width="100%"/>
<br/>
</p>

</p
Ping the alias you created from the Windows 10 client again to observe changes. It should now be able to find "search" and recieve replies from www.google.com since the alias was configured to point to it. You can also use <strong>nslookup</strong> along with your alias to have the network search for the domain name it points to, and all addresses associated with the domain name itself.
<br><img src="https://github.com/user-attachments/assets/f0fd3c15-5a69-4f3d-9542-1581105ae717" height="75%" width="100%"/>
<br/>
</p>

Outdated DNS caches are a common network connectivity roadblock in real-world IT scenarios. Using both your knowledge of the DNS resolution process and OS networking commands, you have the tools to be able to figure out many common networking issues end-users face.
