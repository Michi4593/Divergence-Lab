# Divergence-Lab

## *Stage One*

*Inital Network Topology* 

![Screenshot 2024-05-21 103449](https://github.com/Michi4593/Divergence-Lab/assets/154572004/e8fce86b-8020-4ea5-9989-8224d5b7a81d)

In this stage, I added a Fortinet firewall, 2 ethernet switches, and a windows 10 workstation From there: Link the WAN port on the firewall to the WAN-SWITCH. Link the LAN port on the firewall to the LAN-SWITCH. Link the DMZ port on the firewall to the DMZ-SWITCH. Link the Win10 workstation to the LAN-SWITCH.

## *Stage Two*

 *New Network Topology*
 
 ![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/d28db7fe-ecaf-4637-8770-ddd44f0ca24d)

*Static IP & DNS* 

![332580726-ebcbc22c-dc51-4c2c-bb6b-8870f79b9feb](https://github.com/Michi4593/Divergence-Lab/assets/154572004/7f684d7f-748c-4e31-b118-817c2618d008)

In this screenshot, we had to set a static IP address for our network adapter. The reason a static IP address was needed was because for our network we can't have the IP address changing everytime the adapter turns on and connects to the internet. When information travels to our network and pings our server, traffic will be lost if the IP address is constantly changing using DHCP.

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/5298d61a-1ec6-4cf1-a2dc-d475a174f668)

Step 1 : Add a Win2012r2 server to the lab workspace. Step 2 : Link the Win2012r2 server to the LAN-SWITCH Step 3 and 4 : After setting our static IP address, subnet mask, and default gateway; along with our DNS Server. I had to ping the google.com server to ensure that the DNS server was responding to requests. I pinged 8.8.8.8 (google.com) to ensure there was connectivity to the internet from our IP address. Step 5 and 6 : of this process consisted of me setting up an active directory service to create user accounts (12 total) 2 per user in my group. An admin and an user account.

## *Stage Three* 

*New Network Topology* 

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/9dee4e6a-eaf0-447d-8cd6-99d17c83e827)

Step 1 : As you can see I added another windows server, linked it to the LAN switch.

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/c79d3d65-8f7b-47cf-a011-b8d6c9ddf4bc)

Step 2 : In this server I assigned another static IP address to the new server with the same subnet mask and default gateway. I changed the DNS 1 IP address due to the domain controller acts as the internal DNS server. So if windows2012r2-2 has a request, it reaches out to Windows server 2012r2-1, if win2012r2-1 server doesn't have the DNS query asked for, win2012r2-1 reaches out to the router/firewall who then asks 8.8.8.8 or google.com if they have the answer. After that I Synced the time using NTP (network time protocol). Installed IIS webserver on windows server and joined the server to the domain.

## *Stage  Four*

*New Network Topology*

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/abfa14b1-ddc3-4b61-bef6-b821e4816937)

Step 1 : Add an ubuntu server and link it to the DMZ Switch.

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/36e43e3a-05d4-4bfe-8ee2-0b16a1b7ca30)

Here we set another static IP address to the server. This time it was because we did not have a DHCP server for the DMZ switch. The Ubuntu server was on a different server and subnet from the DHCP server established in the Local Area Network. Our Ubuntu server is also on a DMZ switch which is a public facing network and you want that IP address to be consistent so we had 2 reasons for creating the network this way.

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/65a0be2e-ed6a-4461-8a47-a563d52266dd)

Step 2 : Installing dokuwiki on the Ubuntu server using the terminal on ubuntu.

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/3e29a4bf-9361-415b-b05f-065552140ba6)

This is how dokuwiki looked after installation, and before configuring the webpage.

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/33b851dc-37e3-4dc7-bdf0-c667ab209c4c)

Step 3 : Here I configured the dokuwiki webpage to all of the admin accounts created in stage 2. I configured a documentation report of the network detailing of the firewall, windows 10 workstation, a domain controller (dc) which was also the internal DNS and provided Active Directory (AD) services, an IIS webserver, and a dmz network.

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/f4ca1169-8a4f-4e83-86be-5fb4f4bcab3d)

Step 4 : After configuring the dokuwiki webpage, I configured a Virtual IP (VIP) for the public side of the webserver on the firewall. This picture details how traffic flows through the firewall and what ports certain parts of our traffic are configured on. For example, our DMZ (demilitarized zone) network is configured on port 4 and our LAN (Local Area Network) is configured on port 2.

## *Stage Five*

*New Network Topology*

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/c73a391b-cfbd-4259-90d0-5da8b8406a06)

Step 1 : In this stage like the other I created another windows server and linked it to the DMZ switch.

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/aeea92a0-499d-4a62-b645-a7f53eedd8b3)

Step 2 : Another static IP address was set for the server, along with other static addressing as seen in the photo. After configuring the addressing I synced the computer using the NTP protocol and then joined the server to the domain of our network. Step 3 : In this step an FTP service was installed, however my group and I had to implement steps from a microsoft guide on how to do so, but I cannot provide a screenshot for view, due to the excessive length of the steps.

## *Stage Six*

In this stage there were no changes to the lab workspace. Instead I created a "Hardening Research Notes" tab for us to detail how we could harden the existing network on the Dokuwiki webpage.

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/caf9880b-46c1-45cb-a05f-8d2f360b0933)

This is an example of the hardnening notes. Top right corner shows the rest of the notes for the servers and workstation implemented in the network.

## *Stage Seven* 

In this stage we conducted a vulnerabiity scan on the network using a Greenbone server.

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/13575818-44f4-4f04-af70-cb93bf7791df)

Here are a few of the vulnerabilities on the network. Next will be the documentation of the scans (severity, summary, impact and solution).

![image](https://github.com/Michi4593/Divergence-Lab/assets/154572004/1a2b37c3-0fe6-4851-8b01-00aa6b9581f9)

The documentation report was created based on our vulnerability scan to detail the weaknesses in our network, the severity of the weakness, how it impacts our system, and how we can fix it in the future. Here are just a few of the vulnerability that were shown in the scan. The network was created the way it is in order for this scan to show possible vulnerabilities.

## *Summary*

In this detailed diagram we created a A SMB (small/medium business) network, with a LAN, DMZ, and Guest network. A Windows domain environment. A IIS webserver. A Windows FTP server. A Win10 workstation. A LAMP webserver running on Ubuntu, hosting a wiki. A FortiGate firewall, with a VIP for a DMZ webserver.
