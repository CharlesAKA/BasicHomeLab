<h1>Set up bassic home lab</h1>
 
<h2>✍🏿Description</h2>
I built an active directory administration using server 2019. I used PowerShell automation for providing, maintaning and deprovisioning user account. Created one network dedicated for yje internet on NAT,  one network dedicated for the internal VM.
I will be giving the first virtual machine two network adapters, one is going to Connect to the outside Internet and the other one is going to be used to connect to Sever 2019 on it and then I will sign an IP address. After I assigned IP addressing for the internal network, the external network will automatically IP get addressing from your home network.
After the IP address is set up I will name this server and then instal Active Directory and create the domain.
I will be configuring a map and routing so the clients on the private network can reach the Internet.
Next I will create a DHCP domain controller so when I create the Windows Network it will automatically get an IP address.
I am then going to run a Powershell script that will automatically create around 1000 users.
I will create another virtual machine and instal windows 10 on it. This virtual machine will be connected to the private network, we will name the virtual machine Client 1 and log into it with one of our of our domain accounts.

<br />


<h2>🧑🏿‍💻Environments Used </h2>

- <b>Oracle Virtualbox</b>
- <b>Windows 10 ISO</b>
- <b>Server 2019 ISO</b>

<h2>🚶🏿Walk-through:</h2>
<h3>Part1️⃣ :</h3>

<p align="center">
 
- <b>Name of server DC=DomainController</b>
- <b>One network dedicated for the Internet running on NAT one network dedicated for the internal VM order network</b>
- <b>After installing server 2019 now we create our two NICs and we can set up our IP addressing</b>
- <b> DNS:127.0.0.1 is generic loop back address (pinging yourself) </b>

 <br/>
<img src="https://imgur.com/U6XM618.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />


<br />
 <h3>Part2️⃣ :</h3>
 <p align="center">
   
  - <b>Next install ADDS(Active Directory Domain Services) and create a domain.</b>
  - <b>Create your domain admin account.</b>
  
  </b>
 <br/>
<img src="https://imgur.com/oMjhg30.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/wL9bdJr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

 - <b>Next we are going to install RAS/NAT(Remote Access Server/Network Address Translation) on the domain controller</b>
 - <b>Allow the client to be on the private virtual network but still be able to access the internet through the domain controller</b>
<br />

<img src="https://imgur.com/DFdYrR9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

- <b>Next set up a DHCP server on our domain controller with the scope info. Allow r win10 client to get ip aadd to get on the internet and browse the internet</b>

<img src="https://imgur.com/1STa0sR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<img src="https://imgur.com/dAGNAAi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

- <b>Next we are going to use the PowerShell script to create users</b>
- <b>You can check in the active directory users and computers folder for confirmation that the users are created. In mydomain.com you will see the users folder with the list of created users</b>

<img src="https://imgur.com/EciMC9s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<h3>Part4️⃣ :</h3>
Block attacks<br/>

- <b>Lastly I will create the windows 10 Virtual machine in Virtual Box using an internal NIC</b>
- <b>Check that the internet is working – ping to the internet (ping  www.google.com on command prompt) if this works that means our DNS server is working</b>
- <b>The whole infrastructure is working , we have connectivity all the way to the default gateway which is the domain controller and the domain controller is properly NATing it and forwarding it out to the internet and returning properly </b>
- <b>You can check on the domain controller if you go to the DHCP on the server manager- tools</b>
- <b>You can see that on the domain controller -> IPv4 -> Scope -> Address Leases: There is one lease from our Client1 computer (when we created our client computer and  joined it to the network) it reached out to the DHCP server and requested an address and the DHCP gave it an address to lease. So when the client gets an address it will show up there under the leases.</b>

<img src="https://imgur.com/bgVIVEq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b>After we joined the Client computer to the domain controller you will see on the Active Directory Users and Computers -> Computers: you will see on this folder that it automatically created a Client computer showing that it’s a member of the domain this means that you can use any of the user accounts created to log in to that computer </b>

<img src="https://imgur.com/mQjKMgh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- <b>On  the Client computer can log in using other user and use one of the many accounts created on the PowerShell script to log in.</b>
- <b>With this we have created a mini corporate network, so the Client1 VM would be like a corporate laptop which you can automatically log in using your corporate credentials as it si already on the domain and network </b>
<img src="https://imgur.com/IxZk4sX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

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
