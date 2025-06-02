# Proactive-Threat-Detection-and-Automated-Response-Using-SOAR-and-EDR
Integrating LimaCharlie,Tines and Slack for Next-Generation Security Operations   

## Objective

To design and implement an automated threat detection and response system by integrating Tines as the SOAR platform and Lima Charlie as the EDR solution. The system aims to promptly identify suspicious activities (such as the execution of password recovery tools), generate alerts, and automate notifications through Slack and Email. Additionally, it facilitates rapid incident response by enabling user-driven decisions to isolate affected machines, thereby minimizing potential security threats and improving overall incident handling efficiency.

### Skills Learned 

- Security Automation – Built automated detection and response workflows using Tines, LimaCharlie, slack and email.

- SOAR Integration – Configured Tines for alert handling, notifications, and user-driven actions.

- EDR Usage – Monitored endpoints with LimaCharlie to detect suspicious activity.

- Alerting & Notifications – Set up automated Slack and Email alerts for security incidents.

- Incident Response – Enabled user decisions for actions like isolating compromised machines.

- API Integration – Connected SOAR, EDR, and messaging tools through API-based workflows.

- Threat Detection – Identified risky behaviors  on endpoints.

### Tools used :

- Tines – For building automated security workflows (SOAR platform).

- LimaCharlie – For endpoint detection and response (EDR).

- Slack – For real-time incident notifications and communication.

- Email – For automated alert delivery.

- APIs – To integrate Tines with LimaCharlie and communication platforms.

- LaZagne -  It is an open-source tool used to extract passwords stored on a local computer.
  
- windows VM - installed on virtual box.

### PROJECT MAP :

  ![2 drawio](https://github.com/user-attachments/assets/51e57e63-2e25-424e-9088-751a4623cc57)

### STEP-BY-STEP IMPLEMENTATION :

### STEP 1 

I have downloaded and installed a Windows virtual machine on VirtualBox in step 1 , we can also use cloud platforms like GCP,AZURE,VULTR,etc for windows server.

### STEP 2

Go to the LimaCharlie website , sign up and verify with working email and login with those credentials . Create an new organization in LimaCharlie as follows :

![create organization](https://github.com/user-attachments/assets/5e828b57-710e-44d4-8efc-32486baa5661)

Give Required details:

![create new organization](https://github.com/user-attachments/assets/8ed650cc-3dc9-42e6-abdf-c0180170b125)

### STEP 3

In this step I have Created installation key  :

![create installation key](https://github.com/user-attachments/assets/af7cdbd6-d302-4808-9ff7-1431ca663d26)

### STEP 4

Downloaded the Lima Charlie Windows 64-bit sensor and installed it by using the Powershell with Administrater Privileges on the Windows VM:

![sucessfully created installation key](https://github.com/user-attachments/assets/243abb43-3870-4d3c-8a20-9c350bf0a4b1)


            cd Downloads
                ./hcp_win_x64_release_4.29.0.exe -i <paste_installation_key>

here installation key :

![agent installed (powershell)](https://github.com/user-attachments/assets/738d62f5-c760-4dbb-a5c7-aac92af2b284)

confirmed the installation by services

![confirming by seeing services](https://github.com/user-attachments/assets/21cfcddb-8201-44aa-89eb-9725843a3f31)

we can check at LimaCharlie also by seeing at sensors list:

![our desktop at sensors list](https://github.com/user-attachments/assets/508a310a-184e-4067-811b-fd2ded8788ec)

### STEP 5

Download LaZagne(open-source tool used to extract passwords stored on a local computer) on the windows VM :
      
Lazagne: https://github.com/AlessandroZ/LaZagne

![Downloaded LaZagne](https://github.com/user-attachments/assets/451b54ad-d696-4bbc-82bd-6814e840ee80)

Execute it with admin priveleges on the Powershell or cmd:

![Lazagn executed (powershell)](https://github.com/user-attachments/assets/757daa6d-d311-4e22-914b-7070fd021157)



### STEP 6

In this step , I will create new Detection and Response rule , we can see D & R rules at automation tab :

![D   R rule 1](https://github.com/user-attachments/assets/d2028773-b907-4393-b579-713c1449b221)

click on add rule, to create your own rules :

![new detection and response rule](https://github.com/user-attachments/assets/bc0a3ffb-4021-4008-a9ce-f23521f88e7a)

sucessfully added new rule :

![confirmed D R new rule](https://github.com/user-attachments/assets/ae90ac42-f018-470b-8fff-03fda3d697f6)

Once again execute Lazagne then We can see that LaZagne was detected on Limacharlie with our new Detection and Response rule:

![detected LaZagne 2](https://github.com/user-attachments/assets/75f17bbf-d42d-43c5-b16c-1344f19c5cdb)

we can see LaZagne in the dashboard of LimaCharlie also:

![dashboard ](https://github.com/user-attachments/assets/8463fafc-34f6-40f9-9ce8-87af060a75a2)

### STEP 7

Create a slack account and click on the create workspace:

<img width="899" alt="1" src="https://github.com/user-attachments/assets/11fc740b-00bf-4b74-b938-01d56cbf04ee" />

Give necessary details and click on next:

<img width="928" alt="2" src="https://github.com/user-attachments/assets/bd0b46f7-d2f1-48f9-9f35-83c81a6845b6" />

Create new channel by click on the add channel and create new channel :

<img width="950" alt="3" src="https://github.com/user-attachments/assets/4e9c8d7a-f37b-43c6-9af7-e3b64792c330" />

### STEP 8 

Sign in into the Tines and the welcome page look like as follows:

<img width="788" alt="welcome page of tines after sign (4)" src="https://github.com/user-attachments/assets/d79a702a-9765-44f3-a0b0-c88dee16aa07" />

In Tines, a webhook is a type of trigger action that allows you to receive external data into your Tines story via an HTTP request. It acts as an entry point for automation workflows, enabling other systems or applications to send data into Tines and kick off a sequence of actions.So, i added webhook into the story.

<img width="946" alt="story webhook 5" src="https://github.com/user-attachments/assets/ab11660c-7070-4a10-969e-03d86bd69cf5" />

### STEP 9 

Go to the LimaCharlie and click on the Outputs , add outputs, select destinations, select tines ,
Note: In the Destination host paste the Webhook url from tines as follows: 

<img width="949" alt="6" src="https://github.com/user-attachments/assets/f841599f-7181-4566-b45d-f4330d2c0a25" /> 

### STEP 10 

Add slack app on tines by following steps, go to the dashboard , choose credentials , click on new, select slack app and select Use tines app for slack and click on allow:

![slack app on tines -1](https://github.com/user-attachments/assets/d19c80c9-0a30-4aa1-a082-e969610683bf)

Sucessfully connected slack , userprompt, and email to the webhook and added some data to the message field each of them :

![message added to slack part-5](https://github.com/user-attachments/assets/74899251-f1a1-4228-944c-49de310b509f)

Output message in slack:

![output message to body to slack -part 5](https://github.com/user-attachments/assets/2bafec92-5e66-4bed-b19e-89856baeb077)

Result message in email:

<img width="475" alt="mail alert" src="https://github.com/user-attachments/assets/119d433e-a8a9-473c-83e6-637ef3816831" />

I have added NO Option to the USER PROMPT , whenever user selects no i won't to any thing it just sends message to the slack:

![part-5 no added to user prompt](https://github.com/user-attachments/assets/afb4c0f5-8788-40b9-ba5d-786ef74ddc2b)

Here is the output to the slack whenever user selects the no option:

![part-5 got output in slack for no(user prompt)](https://github.com/user-attachments/assets/a44e7a67-d263-41f7-81ab-8662f2dad38a)

Similar to "NO" option I have given "YES" option to the USER PROMPT and I have configured it to isolate machine whenever user selects yes:

![part-5 yes part completed](https://github.com/user-attachments/assets/e3b7cc76-0f93-4bbd-8c6f-6181f4abe916)

Complete story board:

![Your first story-storyboard](https://github.com/user-attachments/assets/125effc0-e87d-4165-b7a2-75aee531e4c9)


Status of machine before user selects yes:

![part-5 before isolated](https://github.com/user-attachments/assets/71f44cd0-2cfe-4ea6-b2bb-a8eb64322086)

### STEP 11 

Status of machine after user selects yes option:

<img width="941" alt="part-5 Isolated sucessfully" src="https://github.com/user-attachments/assets/ad508461-71e8-4d88-bb17-e38938220649" />

We can see that Isolated machine not pinging:

![part-5 not pinging cmd](https://github.com/user-attachments/assets/fd81f75b-f410-4ec7-b790-56450b32d71f)

Isolated message in the slack:

<img width="765" alt="image" src="https://github.com/user-attachments/assets/e6cb280e-a564-4cb8-8f10-b1490d622731" />














































  


  







