# TryHackMe Redline
Redline will essentially give an analyst a 30,000-foot view (10 kilometers high view) of a Windows, Linux, or macOS endpoint. Using Redline, you can analyze a potentially compromised endpoint through the memory dump, including various file structures. With a nice-looking GUI (Graphical User Interface) - you can easily find the signs of malicious activities.</br>
> Redline was created by [FireEye.](https://fireeye.market/apps/211364)

Here is what you can do using Redline:
- Collect registry data (Windows hosts only)
- Collect running processes
- Collect memory images (before Windows 10)
- Collect Browser History
- Look for suspicious strings
- And much more!

## Introduction
**Q.** Which company created Redline?

Answer: **FireEYE**

## Data Collection
**Q.** What data collection method takes the least amount of time?

Answer: **Standard Collector**

**Q.** You are reading a research paper on a new strain of ransomware. You want to run the data collection on your computer based on the patterns provided, such as domains, hashes, IP addresses, filenames, etc. What method would you choose to run a granular data collection against the known indicators?

Answer: **IOC Search Collector**

**Q.** What script would you run to initiate the data collection process? Please include the file extension.

Answer: **RunRedlineAudit.bat**

**Q.** If you want to collect the data on Disks and Volumes, under which option can you find it? 

Answer: **Disk Enumeration**

**Q.** What is the default filename you receive as a result of your Redline scan?

Answer: **AnalysisSession1.mans**

## The redline Interface
**Q.** Where in the Redline UI can you view information about the Logged in User?

Answer: **System Information**

## Standard Collector Analysis
**Q.** Provide the Operating System detected for the workstation.

![SCA Q1](https://github.com/ankrahjoseph/TryHackMe-Redline/blob/main/Redline/SCA%20Q1.png)

Answer: **Windows Server 2019 Standard 17763**

**Q.** What is the suspicious scheduled task that got created on the computer?

![SCA Q2](https://github.com/ankrahjoseph/TryHackMe-Redline/blob/main/Redline/SCA%20Q2.png)

It looked suspicious because it was created THM-REDLINE\Administrator user. </br>
Answer: **MSOfficeUpdateFa.ke**

**Q.** Find the message that the intruder left for you in the task.

From the same screenshot, under the comment tab.</br>
Answer: **THM-p3R5IStENCe-m3Chani$m**

**Q.** There is a new System Event ID created by an intruder with the source name "THM-Redline-User" and the Type "ERROR". Find the Event ID #.

![SCA Q3](https://github.com/ankrahjoseph/TryHackMe-Redline/blob/main/Redline/SCA%20Q3.png)

I went to the Event Logs section then searched for "THM-Redline-User" and selected source as the search tab.</br>
Answer: **546**

**Q.** Provide the message for the Event ID.

On the same Event Log, you will find the answer in the message tab </br>
Answer: **Someone cracked my password. Now I need to rename my puppy-++-**

**Q.** It looks like the intruder downloaded a file containing the flag for Question 8. Provide the full URL of the website.

![SCA Q4](https://github.com/ankrahjoseph/TryHackMe-Redline/blob/main/Redline/SCA%20Q4.png)

I went to the File Download History section and saw the flag.txt file </br>
Answer: **https://wormhole.app/download-stream/gI9vQtChjyYAmZ8Ody0AuA**

**Q.** Provide the full path to where the file was downloaded to including the filename.

On that same line, the target directory shows where the downloaded file was saved </br>
Answer: **C:\Program Files (x86)\Windows Mail\SomeMailFolder\flag.txt**

**Q.** Provide the message the intruder left for you in the file.

![SCA Q5](https://github.com/ankrahjoseph/TryHackMe-Redline/blob/main/Redline/SCA%20Q5.png)

Use the file path to locate the file and opened it to find the message </br>
Answer: **THM{600D-C@7cH-My-FR1EnD}**

## IOC Search Collector

**Q.** What is the actual filename of the Keylogger? 

Answer: **psylog.exe**

**Q.** What filename is the file masquerading as?

Answer: **THM1768.exe**

**Q.** Who is the owner of the file?

This can be found in the last screenshot provided in the reading for this task.</br>
Answer: **WIN-2DET5DP0NPT\charles**

**Q.** What is the file size in bytes?

This can be found in the last screenshot provided in the reading for this task.</br>
Answer: **35400**

**Q.** Provide the full path of where the .ioc file was placed after the Redline analysis, include the .ioc filename as well

This can be found in the 3rd to the last screenshot provided in the reading for this task.</br>
Answer: **C:\Users\charles\Desktop\Keylogger-IOCSearch\IOCs\keylogger.ioc**

## IOC Search Collector Analysis

**Q.** Provide the path of the file that matched all the artifacts along with the filename.

![ISCA Q1](https://github.com/ankrahjoseph/TryHackMe-Redline/blob/main/Redline/ISCA%20Q1.png)

After creating the IOC and using it to generate the report, it tool about 15 minutes to complete.I got one hit.</br>
Answer: **C:\Users\Administrator\AppData\Local\Temp\8eJv8w2id6IqN85dfC.exe**

**Q.** Provide the path where the file is located without including the filename.

Answer: **C:\Users\Administrator\AppData\Local\Temp**

**Q.** Who is the owner of the file?

Answer: **BUILTIN\Administrators**

**Q.** Provide the subsystem for the file.

Answer: **Windows_CUI**

**Q.** Provide the Device Path where the file is located.

Answer: **\Device\HarddiskVolume2**

**Q.** Provide the hash (SHA-256) for the file.

The IOC report provided us with the MD5 hash so I went to [virustotal](https://www.virustotal.com/gui/file/57492d33b7c0755bb411b22d2dfdfdf088cbbfcd010e30dd8d425d5fe66adff4/details) and searched for the md5 hash and found details about the file.

![Virus Total](https://github.com/ankrahjoseph/TryHackMe-Redline/blob/main/Redline/VirusTotal.png)

Answer: **57492d33b7c0755bb411b22d2dfdfdf088cbbfcd010e30dd8d425d5fe66adff4**

**Q.** The attacker managed to masquerade the real filename. Can you find it having the hash in your arsenal? 

The [virustotal](https://www.virustotal.com/gui/file/57492d33b7c0755bb411b22d2dfdfdf088cbbfcd010e30dd8d425d5fe66adff4/details) page provided the names for the file.</br>
Answer: PsExec.exe

## Endpoint Investigation
**Q.** Can you identify the product name of the machine?

![ED Q1](https://github.com/ankrahjoseph/TryHackMe-Redline/blob/main/Redline/ED%20Q1.png)

Answer: **Windows 7 Home Basic**

**Q.** Can you find the name of the note left on the Desktop for the "Charles"?

![ED Q2](https://github.com/ankrahjoseph/TryHackMe-Redline/blob/main/Redline/ED%20Q2.png)

I navigated to the **File System** Section and selected Desktop under the user Charles.</br>
Answer: **_R_E_A_D___T_H_I_S___AJYG1O_.txt**

**Q.** Find the Windows Defender service; what is the name of its service DLL? 

![ED Q3](https://github.com/ankrahjoseph/TryHackMe-Redline/blob/main/Redline/ED%20Q3.png)

I navigated to the **Windows Serviced** tab and searched for 'windows defender'</br>
Answer: **MpSvc.dll**

**Q.** The user manually downloaded a zip file from the web. Can you find the filename? 

![ED Q4](https://github.com/ankrahjoseph/TryHackMe-Redline/blob/main/Redline/ED%20Q4.png)

I navigated to the **File Downloaded History** section and searhed for '.zip'</br>
Answer: **eb5489216d4361f9e3650e6a6332f7ee21b0bc9f3f3a4018c69733949be1d481.zip**

**Q.** Provide the filename of the malicious executable that got dropped on the user's Desktop.

Back on the **File System** section, I found the malicious executable.</br>
Answer: **Endermanch@Cerber5.exe**

**Q.** Provide the MD5 hash for the dropped malicious executable.

Answer: **fe1bc60a95b2c2d77cd5d232296a7fa4**

**Q.** What is the name of the ransomware? 

![Virus Total2](https://github.com/ankrahjoseph/TryHackMe-Redline/blob/main/Redline/Virus%20Total%202.png)

I searched the md5 hash of the file on [virustotal]() and found the name of the ransomware. </br>
Answer: **Cerber**
