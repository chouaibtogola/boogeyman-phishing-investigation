# boogeyman-phishing-investigation
DFIR investigation of a phishing attack involving malicious VBA macros, staged malware delivery, C2 communication, and persistence analysis using Volatility and Olevba.

## Executive Summary
Below is the Mail received by Maxine Beck, a Human Resource Specialist working for Quick Logistics LLC, who received an application from one of the open positions in the company . Attached to the email was a malicious Microsoft Word document named Resume_WesleyTaylor.doc, disguised as a candidate resume.She opened it, not knowing the attachment was malicious and compromised her workstation.
<img width="975" height="574" alt="image" src="https://github.com/user-attachments/assets/9039eaa8-ec97-4b4f-a480-719ff8566ca1" />
<img width="975" height="430" alt="image" src="https://github.com/user-attachments/assets/7b41056c-1ab6-4191-b87b-6f699919843f" />

Once executed , the victim inadvertently executed VBA macros. The macros downloaded a second-stage payload from a remote attacker-controlled server and executed it on the victim’s machine. 

Following execution, the malware established outbound communication with a command-and-control (C2) server, allowing the attacker to maintain remote access and potentially deploy additional malicious activity. Shortly after the initial compromise, the attacker created a scheduled task to maintain persistent access to the infected system.

#How DO We Go About It
let's check the MD5 hash of the malicious document first 
<img width="956" height="74" alt="image" src="https://github.com/user-attachments/assets/58ba35ac-ac71-41e2-b191-6968660536f4" />

Let's run the olevba to check for malicious contents in microsoft office files
<img width="1385" height="706" alt="image" src="https://github.com/user-attachments/assets/d38b0ff1-edc9-47f3-900a-416bdee791c2" />
we can see the malicious link that download the stage 2 payload. We see as well that wscript.exe is the payload that executed it 

we will now check its unique identifier (PID) 
<img width="1263" height="88" alt="image" src="https://github.com/user-attachments/assets/55508942-9219-4fde-9a48-cc6ecd8c9170" />
now do you know we can check which process led to the former? Here is how we go about it 
<img width="1383" height="150" alt="image" src="https://github.com/user-attachments/assets/18d536cc-abb6-4159-b128-7dc03f05e920" />
<img width="1403" height="276" alt="image" src="https://github.com/user-attachments/assets/fb683924-9c4c-4899-b5ba-1d8f5628f9a4" />

let us see how the c2 connection was established 
<img width="1335" height="141" alt="image" src="https://github.com/user-attachments/assets/6369b766-39d0-4281-901c-690c5feba5ad" />
now below is its IP address with the listening port 
<img width="1385" height="652" alt="image" src="https://github.com/user-attachments/assets/c914d0be-530d-4adb-97cd-2bc5dba6aab4" />

we can check the full path of the malcious attachment based on memory dump 
<img width="1392" height="177" alt="image" src="https://github.com/user-attachments/assets/02b1ca50-6aa6-4910-af08-81ef818929d5" />

