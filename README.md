# boogeyman-phishing-investigation
DFIR investigation of a phishing attack involving malicious VBA macros, staged malware delivery, C2 communication, and persistence analysis using Volatility and Olevba.

## Executive Summary
Below is the Mail received by Maxine Beck, a Human Resource Specialist working for Quick Logistics LLC, who received an application from one of the open positions in the company . Attached to the email was a malicious Microsoft Word document named Resume_WesleyTaylor.doc, disguised as a candidate resume.She opened it, not knowing the attachment was malicious and compromised her workstation.
<img width="975" height="574" alt="image" src="https://github.com/user-attachments/assets/9039eaa8-ec97-4b4f-a480-719ff8566ca1" />
<img width="975" height="430" alt="image" src="https://github.com/user-attachments/assets/7b41056c-1ab6-4191-b87b-6f699919843f" />

Once executed , the victim inadvertently executed VBA macros. The macros downloaded a second-stage payload from a remote attacker-controlled server and executed it on the victim’s machine. 

Following execution, the malware established outbound communication with a command-and-control (C2) server, allowing the attacker to maintain remote access and potentially deploy additional malicious activity. Shortly after the initial compromise, the attacker created a scheduled task to maintain persistent access to the infected system.
