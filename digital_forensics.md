# Digital forensics 2009 M57-Patents Scenario

## Objective
The primary objective of this project is to conduct a [**digital forensic investigation of the M57 Patents data breach**](https://digitalcorpora.s3.amazonaws.com/corpora/scenarios/2009-m57-patents/docs/M57-Patents-Exfiltration.pdf) using the Autopsy software to analyze digital evidence and determine how confidential research was leaked. The key goals include:
- **Identifying the perpetrators**: Uncovering both the internal employees and external parties involved in stealing and sharing confidential data.
- **Analyzing digital artifacts**: Investigating hard drives, USB drives, emails, encrypted ZIP files, and steganographic images to discover how stolen information was accessed, hidden and transmitted as well as to whom.
- **Recovering evidence for prosecution**: Documenting a clear, traceable chain of evidence to prove the data breach and support potential criminal proceedings.

The [2009 M57-Patents scenario](https://digitalcorpora.org/corpora/scenarios/m57-patents-scenario/) is provided by Digital Corpora. 

### Skills Learned

- Advanced understanding of digital forensics concepts
- Proficiency in analyzing and interpreting digital artifacts.
- Improving understanding the concept of stegnography

### Tools Used

- *Autopsy* from the sleuthkit for forensic searches of computer storage volumes.
- STEG Program *Invisible Secrets* for stegnography.

## Steps
1. First things first getting a briefing of the situation by reading the [exercise slides](https://digitalcorpora.s3.amazonaws.com/corpora/scenarios/2009-m57-patents/docs/M57-Patents-Exfiltration.pdf).
2. Creating a new case in autopsy and adding the latest images of the different hard drives.
3. The real investigation starts with getting an overview of the data. As this case is about communication and sending data the e-mails are a logical point to start digging.
   
 <img width="282" height="673" alt="overview_of_data" src="https://github.com/user-attachments/assets/31b30983-1823-46e5-92fa-69deb54a1733" />

*Ref 1: Autopsy Overview of the Files


4. By sorting the mails by "delivered to" to easily scan the individual entries. A few addresses look interesting:  
   -  "rubinfritz31@mail.com", "alix.pery@yahoo.com" because they are a private addresses -> nothing interesting, a new colleague introducing himself and private stuff.
   -  "linuxuser-admin@www.linux.org.uk" its a cryptic address -> only normal e-mailing
   -  "andy@swexpert.com", "jamie@project2400.com" another company -> less suspicious in the first place but after overlooking the content either is a hit.
  Bookmarking the e-mails to easily find them later on in the investigation.

 <img width="1157" height="614" alt="e-mails" src="https://github.com/user-attachments/assets/f258025e-737b-4791-b034-9f67d6a19316" />
*Ref 2: overview of the e-mails, including bookmarks


5. After reading through the e-mail correspondence between **andy@swexpert.com** and Charlie, one of the employees at m-57, it was pretty obvious charlie tries to blackmail him. A password protected zip folder was sent with the initial mail. The password should be send in the next mail as a picture. Indeed a picture was sent shortly after but without any obvious password, the name *microscope1* itself was not the password as well as *R232* as the name of the microscope, leading to further investigations. In the hex-format the password *immortal* was visible. 

<img width="1185" height="434" alt="blackmailing" src="https://github.com/user-attachments/assets/e48c0284-2d28-4602-abde-56e9ecef224b" />
*Ref 3: Initial e-mail form Charlie to the blackmailed.

<img width="1185" height="451" alt="Password_blackmailing" src="https://github.com/user-attachments/assets/4c6b4a9e-c0a0-45b7-ac09-ab1f0e7ebadc" />
*Ref 4: Picture that was send including the password.

<img width="688" height="526" alt="Hex_microscope" src="https://github.com/user-attachments/assets/e1360ef5-d3cb-4ddd-8ee6-d15d481bd4ce" />

*Ref 5: hex-format of the picture

6. In the zip file the front pages of two patents were shown.
   
<img width="882" height="617" alt="Pattent" src="https://github.com/user-attachments/assets/1cf4062d-95c1-46d9-a922-913fb6577bc3" />

*Ref 6: Inside the zip file

7. Going on with reading through the correspondence between Charlie and Jaime from project2400. Charlie offers him information , if he gets paid his normal rate. Indicating Charlie had done things like this before.
<img width="1184" height="319" alt="SellingInformation" src="https://github.com/user-attachments/assets/ea8ae2ae-c871-4740-a769-0bd5b7ce0042" />
*Ref 7: E-Mail from Charlie to Jaime.
PS. funny how he shortens their names with the initials but writes from his personal work account.

8. It seems Charlie got the money and sends Jaime the information in another E-Mail in form of another picture. He remembers Jamie he should use the steg program. On Charlies Computer a program is installed, that is called 'Invisible secrets 2.1', which did not look familiar. After researching it on the internet it was clear this program was used to hide these picture.

9. After installing Invisible Secrets 2.1 and extracting the astronaut picture a text file was revealed.

<img width="741" height="384" alt="Janie" src="https://github.com/user-attachments/assets/ffa9bf6c-7e3b-4200-b3f2-4aeaf45b2f4b" />

*Ref 8: Revealed textfile
