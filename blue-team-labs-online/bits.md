---
description: https://blueteamlabs.online/home/investigation/33
---

# BITS

## Scenario

> Using BitsParser from FireEye to retrieve BITS jobs, can you help the SOC identify persistence actions conducted on a compromised host? **Read the "READ ME!.txt" file in the Investigation folder on the Desktop.** \
> \
> **Reading Material:**\
> [FireEye Blog Post](https://www.mandiant.com/resources/attacker-use-of-windows-background-intelligent-transfer-service)\
> [BitsParser GitHub Page](https://github.com/fireeye/BitsParser)

BITS is a living off-the-land binary that is used by software such as web browsers to periodically download updates. It can however be abused for lateral movement, tool deployment, and persistence.

To start this lab we will refer to the BitsParser GitHub Page for documentation on how to use it.

{% hint style="info" %}
BitsParser is a Python 3 script that can parse Windows Background Intelligent Transfer Service database files and extract job and file information. It supports both the original custom database format as well as the ESE database format used on Windows 10 systems.
{% endhint %}

I also opened up the Investigation folder on the desktop and found a `READ ME!` file. This file contains information relevant to the lab, including what BITS as well as some key points relating to BITS.

We will be using an administrator-level Command Prompt since to execute BitsParser.py, you need administrator privileges. To do this we right click the cmd file and select Run as Administrator

Before the BitsParser is able to retrieve the BITS jobs, the BITS service that is currently running needs to be stopped. To do this we can launch the Task Manager by simply right clicking the taskbar and selecting Task Manager. Open the Services tab and located the BITS service, which we can see is running under the netscvs group. Right click it and click Stop.

![](<../.gitbook/assets/Screen Shot 2022-03-08 at 10.12.50 PM.png>)

We will now be using the cmd (Remember to run as an administrator). Use the command cd to change the directory to the directory containing the BitsParser python script.&#x20;

Run the following command:&#x20;

`cd C:\Users\BTLOTest\Desktop\Investigation\BitsParser-master`

Entering the `dir` command shows the contents of the BitsParser-master folder. Here we can see the `BitsParser.py` python script.

To run this script, enter this command in to the cmd:

`python BitsParser.py --carveall > output.txt`

The `--carveall` flag will provide more information. The script is also known to not properly output the results when using their `-o filename` flag, this is why we used `> output.txt` instead.

### Questions

{% hint style="info" %}
Question 1) A popular GitHub Repo for Windows privilege escalation is WinPEAS. Can you find any file downloads for winPEAS.bat in the BitsParser output? What is the associated job name? (Format: BITSJobName)_(3 points)_

💡Answer: **privesctools**
{% endhint %}

After the command is done running, open the `output.txt` file which should be in same folder as the python script we just ran. You can also open it using cmd by entering the command `"output.txt"`, be sure to include the quotation marks. Here we can see different jobs were carved, we are looking for the job associated with winPEAS.bat, press `ctrl+f` and type in `winPEAS.bat`&#x20;

![](<../.gitbook/assets/Screen Shot 2022-03-08 at 10.32.25 PM.png>)

Here we can see winPEAS.bat was downloaded, we know this because by looking at the "`JobType"`, we can see the value is "`download"`. We also see `"JobName": "privesctools"`, there is our answer!

{% hint style="info" %}
Question 2) What is the Creation Time of this job? (Format: YYYY-MM-DDTHH:MM:SSZ)_(3 points)_

_💡_Answer: **2022-01-07T13:32:19Z**
{% endhint %}

To get this answer, we are still using the previous text file `output.txt` scroll down below and you will find the `"CreationTime": "2022-01-07T13:32:19Z"`field which gives us our answer.

![](<../.gitbook/assets/Screen Shot 2022-03-08 at 10.38.01 PM.png>)
