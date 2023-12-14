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

1. Create resources 
2. Observe ICMP traffic 
3. Observe SSH traffic 
4. Observe DHCP traffic
5. Observe DNS traffic
6. Observe RDP traffic 

<h2>Actions and Observations</h2>

<h3>1. Creating the resources</h3>

To start off, I logged into my Azure account and headed over to resource groups in order to create one to hold my virtual machines. For this project I created one Windows 10 pro (21H2) machine and a Linux (Ubuntu Server 20.04) machine. I made sure Azure created the Windows machine's virtual private network and subnet before creating the Ubuntu machine. This step was crucial to open the line for communication between them. For the Windows machine, I allowed port 3389 to be open to enable the remote desktop feature. In the Ubuntu machine, I enabled port 22 to enable the secure shell feature. After the creation of my resources, I verified that both machines were placed in the same virtual network. 

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/85a405da-f87b-464b-bf13-59faaef72930)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/aacc5ba2-d110-4a76-9b5a-d11812a5b0ce)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/06674bad-dd36-4bd9-b985-256064d26e32)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/3d431218-7e41-4ff6-8b99-f6ab5ef7e936)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/e18e3b8b-50ca-47e4-b237-bfb82e699a9c)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/012a2c98-da92-4083-933d-922fdce054f4)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/7720402e-61b0-42b9-888e-2f4c3f63ced4)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/a1e50a93-86e6-4e3c-a674-5d0c926d586b)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/638ca07e-48aa-4221-8baa-3d4f41a64f3f)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/f1d08824-c08f-4fcc-8fea-b3e4de18710c)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/e202f25c-19b6-4614-a162-f6be814edc49)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/a00f3e9e-53b0-425e-8a00-384a6b3c8dbc)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/aa95c668-d166-489f-bf1d-824d2ea6aeaf)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/e24fa911-ae57-4297-98ce-21ce0b3ff9f6)




<h3>2. Observe ICMP traffic</h3>

Using the Windows machine's private IP address taken from my Azure Network Watcher, I connected to my Windows machine via Remote Desktop. I proceeded to downloading and installing Wireshark using my browser. Wireshark is a network protocol analyzer used to capture packets from a network connection. This is the application I utilized to observe what communications were being transmitted behind the scenes in my own network connections. 

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/10ad71b4-7483-471f-991c-019b98523eb2)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/b4f3304c-6ba7-444d-892e-ab3932685cd7)




After wireshark was installed and running, I selected the Ethernet option and clicked on the shark fin icon in the top left corner of the app to input an Internet Control Message Protocol filter. A ping, comprised of ICMP messages, is the method used to measure the communication latency between networks or devices (nodes). An ICMP is essentially a packet with random data sent to a destination to communicate any errors to the source. 

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/5fa4b9a2-e37c-4f06-8690-ab9738c5d680)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/e186db3c-8a45-425f-83c0-5f1142c56342)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/fe8cb4c2-b045-4325-ab93-31166d272d06)






In this case, the ICMP messages will reflect in Wireshark and I was able to view the transmissions issued within the source and destination address. To view the messages, I opened up my WIndows Powershell command line and issed a Ping to my Ubuntu machine with its private IP address.

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/3a88a189-2e3e-416c-9026-cebd0561508a)


I was also able to observe ICMP traffic when I pinged a website address such as www.google.com

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/239ca0d0-33a1-4c40-8baf-161d4862090f)


To explore the network security groups feature, I initiated a perpetual nonstop ping using "ping IP address -t" in the command line. Once this was going I switched over to the VM's virtual firewall in Azure to set a new rule to block ICMP transmissions form anywhere. The NSG feature lets me set rules to allow or deny cerrtain protocols and port numbers. After I verified that the ICMP traffic has ceased, I enabled the rule once again to analyze the traffic once more and then stopped the endless incoming ICMP packets using "ctrl + c".  

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/5d6c48d1-4351-4094-8e16-a590a93bd71e)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/e7323ecd-391d-4d2a-80ac-1f5ede093fad)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/8a638bb3-fbaf-4a29-9297-a1199ef4f246)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/8e039bb5-7dab-41ed-b6b6-65f36f826cd7)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/0068f9c4-6c1d-4e81-9b54-e0ce20ef7c5d)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/a60681c9-d1d5-42fe-8304-56dbff9d68d9)



<h3>3. Observe SSH traffic</h3>

Secure Shell or SSH is basically a secure remote shell that is used for communication between nodes. This time I cleared out my filter in Wireshark and typed in SSH to filter for packets going through port 22. Another way to filter for ssh traffic is to use filter "tcp.port == 22".  I then opened up my Powershell terminal and opened up a connection to my Ubuntu machine through SSH. The format needed to make this connection in the command line is:

ssh username@IPaddress

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/73cbbc35-bbbf-46fd-88a4-131396b3c923)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/e67d9963-9267-4421-a2fb-a7d75a43cb23)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/778455cd-3c5e-41c7-b619-8eafe38bc10d)



Once the connection is made i was able to type in commands in the Linux machine and observe the traffic data within Wireshark. To exit the Linux machine, I simply typed in "exit" and pressed "enter".

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/30b68c47-aade-4318-abad-f9f4db49ce47)


<h3>4. Observe DHCP traffic</h3>

The next filter I applied was for the DHCP protocol. Dynamic Host Configuration Protocol or DHCP is a network management protocol that automatically assigns IP addresses and other communication parameters to devices connected to the network. From my Windows machine's command line I was able to issue a new Ip address using the following command: 

ipconfig /renew 

As the results came back I analyzed the activity going through Wireshark activated by the command. 

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/bff78879-4443-47a1-81cc-3628f2ffc070)


<h3>5. Observe DNS traffic</h3>

In this observation I filtered for DNS traffic within Wireshark. Domain Name Service or DNS is the system that converts website domain names (hostnames) into numerical values (IP address) so they can be found and loaded into your web browser. To achieve this I used the command line in Powershell and typed in the command: 

nslookup www.google.com 

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/4ec54dc4-b281-4209-b364-da48a450c9dd)

![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/5271337d-cfbe-4ae4-906c-33de6b480f22)




Then another lookup for Disney:

nslookup www.disney.com


![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/8a3754e3-fe32-4151-ab96-cea00a0a2555)


Another way you can filter DNS traffic in Wireshark is the following: 

udp.port == 53




<h3>6. Observe RDP traffic</h3>

The last filter I applied to Wireshark was for RDP or Remote Desktop traffic. Remote desktop is a software or operating system feature that allows a user to access and control another device from a distance. I used the filter: 

tcp.port == 3389

The traffic spam for RDP is nonstop because the protocol displays a live stream from node to node. 


![image](https://github.com/jonathansantacruz3/azure-network-protocols/assets/151465848/e176a52e-f300-4bb9-acad-c9b215f9095f)

Thanks for reading !
