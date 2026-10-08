# NETWORK ANALYSIS

## Objective
Analysis of logged network traffic to detect malicious activities like command and control communication, data breaches or scanning activities.
In a scenario several signature hits for NetSupport RAT from 45.131.214.85 over TCP port 443 were shown in SIEM system. The activity started on 28-02-2026 at 19:55.

### Skills Learned

- Advanced understanding of protocols like TCP/IP, DNS or HTTP/S
- Proficiency in analyzing and interpreting network logs.
- Ability to recognize indicators of compromise (IOC).
- Enhanced knowledge of network protocols and security vulnerabilities.

### Tools Used

- Network analysis tools (such as Wireshark) for capturing and examining network traffic.


## Steps
The characteristics of the environment are:
- LAN segment range:  10.2.28.0/24   (10.2.28.0 through 10.2.28.255)
-  Domain:  easyas123.tech
-  AD environment name:  EASYAS123
-  Active Directory (AD) domain controller:  10.2.28.2 - EASYAS123-DC
-  LAN segment gateway:  10.2.28.1
-  LAN segment broadcast address:  10.2.28.255

1. the captured traffic showed 15512 individual packages. Known from the SIEM system alert the RAT attack probably came from 45.131.214.85.

<img width="763" height="612" alt="first_look_at_the captured_packages" src="https://github.com/user-attachments/assets/236527cc-7ee1-4e8a-8f7c-79ac90d82f9e" />

*Ref 1: the unfiltered pcap package

2. Filtering the captured traffic for the source of said IP range it reveals a HTTP connection was built with 10.2.28.88 as seen in the Picture below. 

<img width="760" height="616" alt="filtered_for_source" src="https://github.com/user-attachments/assets/51cda4f3-0e3d-41c0-8c7e-bd25b88aa810" />

*Ref 2: network traffic filtered for source == 45.131.214.0/24

3. Looks like a persistent HTTP connection was established. The first packages show a synchronize followed by a synchronize-acknowledge and an acknowledge package. In the further package stream another connection is not shown.

<img width="738" height="125" alt="http_session" src="https://github.com/user-attachments/assets/8fdd4d06-13d3-4a96-8769-74d92e5f419c" />

*Ref 3: establishing a persistent HTTP session

4. Looking into the packages it reveals the MAC address of the infected system is 00:19:d1:b2:4d:ad. Or at least of the next hop in the direction of this system.

<img width="706" height="126" alt="MAC_address" src="https://github.com/user-attachments/assets/641d87f1-4433-4aa6-b999-fb75a520b42c" />

*Ref 4: first package send from the system under investigation

5. Searching for NetBIOS Name Service (nbns) of 10.2.28.88 the host name of the windows client is revealed: DESKTOP-TEYQ2NR

<img width="729" height="497" alt="nbns" src="https://github.com/user-attachments/assets/c529b652-eff9-420b-a924-0ed00d690578" />

*Ref 5: filtering for "nbns" and the IP-address of the target

6. Searching for kerberos.SNameString of 10.2.28.88 the user account name of the windows client is revealed: brolf

<img width="746" height="575" alt="kerberos CNameString" src="https://github.com/user-attachments/assets/24147f3f-8029-47ef-aac8-ba41779540c6" />

*Ref 6: filtering for "nbns" and the IP-address of the target
   
7. Searching for "Rolf" in the packet details the full name of the user account is revealed: Becka Rolf

<img width="752" height="605" alt="full_name" src="https://github.com/user-attachments/assets/1b4f629b-2869-412e-a48f-e54dc7183ba8" />

*Ref 7: Searching cap sensitive for "Rolf" as string in the package details.
