<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1 - Create two VMs one using Windows 10 (21H2), the other using Ubuntu Server 20.04.
- Step 2 - On the Windows VM Download Wireshark (everything will be installed on default settings).
- Step 3 - Open Wireshark, it will provide two options click on Ethernet and then click on the shark fin at the top left under the 'File' option.
- Step 4 - This will show all of the live traffic that is happening on the VM, on the search bar on top type in ICMP this way it filter it so we only see ICMP traffic.
- Step 5 - Now we will Ping VM2 from VM1 but to this we need to Find out the Private I.P Address of VM2 so on Azure if you click VM2 it will show all of its Specs. <img width="1440" alt="Screen Shot 2023-11-06 at 1 54 55 PM" src="https://github.com/Danial-Dawood/Network-Security-Groups-NSGs-and-Inspecting-Network-Protocols/assets/149525309/d502a56f-dcb4-4cc1-ab8b-37c76b052d5f">
- Step 6 - If you look at the lower right of the ScreenShot it Says 'Private I.P 10.0.0.5' - this is what we need.
- Step 7 - Then going back into VM1 open up PowerShell (you can just type in PowerShell in the search bar on the bottom left)
- Step 8 - With this we will Ping VM2 this is what the command will look like 'ping 10.0.0.5(VM2 Private I.P Address)
<img width="1440" alt="Screen Shot 2023-11-06 at 2 02 54 PM" src="https://github.com/Danial-Dawood/Network-Security-Groups-NSGs-and-Inspecting-Network-Protocols/assets/149525309/851b084e-b0df-47d2-a8f9-c5b7faf18390">
- Step 9 - This is what the traffic looks like going from one VM to the other  <img width="1440" alt="Screen Shot 2023-11-06 at 2 04 51 PM" src="https://github.com/Danial-Dawood/Network-Security-Groups-NSGs-and-Inspecting-Network-Protocols/assets/149525309/5f3ca46c-af89-4748-bed9-575466ccedad">
- Step 10 - Now we will ping Google, similar command type in 'ping www.google.com -4' (the -4 at the end of it is so that it Ipv4 Address)<img width="1440" alt="Screen Shot 2023-11-06 at 2 10 46 PM" src="https://github.com/Danial-Dawood/Network-Security-Groups-NSGs-and-Inspecting-Network-Protocols/assets/149525309/c7638c03-44b9-4a1c-99d8-d7dcfd34bf57">
- Step 11 - We can even see what is sent in this 'Ping' Message by Clicking on your Private I.P on one of the Pings then click the drop down menu on 'Internet Control Message Protocol' then the drop down menu on 'Data' It will show what was sent and its just the alphabet.<img width="1440" alt="Screen Shot 2023-11-06 at 2 36 02 PM" src="https://github.com/Danial-Dawood/Network-Security-Groups-NSGs-and-Inspecting-Network-Protocols/assets/149525309/049ce454-0857-4aed-8422-b50f7509c371">
- Step 12 - Clear all of this date on WireShark by clicking the Green shark fin at the top left. Now we will send a perpetual Ping to VM2 the command will be "ping 10.0.0.5(private I.P of Vm2) -t"
- Step 13 - Now we will go Vm2's FireWall and disable Icmps(just to see how Firewalls work and learn a little more about them.) Go into Azure and at the top type in 'Network Security Groups' and the click 'VM2-nsg' next click 'Inbound Security Rules.' This is will Make it so it will block we sent from VM1 <img width="1440" alt="Screen Shot 2023-11-06 at 2 49 46 PM" src="https://github.com/Danial-Dawood/Network-Security-Groups-NSGs-and-Inspecting-Network-Protocols/assets/149525309/0c6de651-f934-4135-ae4e-92cf365d46b3">
- Step 14 - If we go to Vm1 and check WireShark we can see that that the ping is no longer being 'Echoed' from VM2 so it will failing <img width="1440" alt="Screen Shot 2023-11-06 at 2 53 27 PM" src="https://github.com/Danial-Dawood/Network-Security-Groups-NSGs-and-Inspecting-Network-Protocols/assets/149525309/7e06c464-ba4f-45f3-8b3c-02059dd63633">
- Step 15 - Now go back to NSG and set the ICMP rule from deny to allow and then we can see the request be completed again.<img width="1440" alt="Screen Shot 2023-11-06 at 2 57 41 PM" src="https://github.com/Danial-Dawood/Network-Security-Groups-NSGs-and-Inspecting-Network-Protocols/assets/149525309/4016446a-5252-4cbe-8717-d7f529790454">
- Step 16 - Now cancel the ping by clicking on the powershell program and clickking 'Control + c ' next we are going to explore ssh traffic, ssh allows us to get control of another computers command line. Go to the Wireshark and where we had typed in 'ICMP' we ar now going to type in 'SSH'. Now we will log into Vm2 via SSH from vm1, so go Powershell and type "'ssh' + 'username for vm2@''Private I.P Address for vm2' So for me it will lok like 'ssh danny@10.0.0.5' you can see as soon as you try to connect it will pop up with SSH traffic in wireshark. <img width="1440" alt="Screen Shot 2023-11-06 at 3 44 24 PM" src="https://github.com/Danial-Dawood/Network-Security-Groups-NSGs-and-Inspecting-Network-Protocols/assets/149525309/900c4ecf-113f-445f-8133-1a2154e3f31c">
- Step 17 - When logging in the password wont show up so you will just have to have faith that your typing in the correct password but it should pop up with a message like this when done <img width="1440" alt="Screen Shot 2023-11-06 at 3 50 21 PM" src="https://github.com/Danial-Dawood/Network-Security-Groups-NSGs-and-Inspecting-Network-Protocols/assets/149525309/4c5212fe-4e90-4a2e-9b4a-1ebbc3d1b742">
- Step 18 - Just another way to be sure youre in VM2 at the bottom of PowerShell it will say your 'username@VM2' and now whenever you type another into Powershell you can acutally see it spam traffic into Wireshark(reason being information is being sent from VM1 to VM2)
- Step 19 - To close the connection just type 'exit' wireshark
- Step 20 - Next we are going to see some DHCP traffic so type in DHCP where it now say SSH. Then into PowerShell type in 'IPconfig/Renew' this is give Vm1 a new I.P Address. A the same time we will be able to obseve DHCP traffic being sent. As well as our I.P Address being changed from10.0.0.4 to 10.0.0.1 <img width="1440" alt="Screen Shot 2023-11-06 at 4 11 13 PM" src="https://github.com/Danial-Dawood/Network-Security-Groups-NSGs-and-Inspecting-Network-Protocols/assets/149525309/a75d57e5-7e13-406b-b7d7-c9e4d772ad39">





 




