
# Class 10 — EC2 Hardening (Server ko Secure Banana)

## 1. What Is EC2?

### Definition
Amazon Elastic Compute Cloud (Amazon EC2) is an AWS service that provides virtual servers called instances for running applications and workloads in the cloud.

### Roman Urdu Explanation
Amazon EC2 AWS ki service hai jis ki madad se hum cloud mein virtual server create kar sakte hain.

Is server par hum Linux ya Windows operating system chala sakte hain, software install kar sakte hain aur websites ya applications host kar sakte hain.

### Example
Agar aap AWS par website host karna chahti hain, to aap EC2 instance create karke us par Apache ya Nginx install kar sakti hain.

Lekin server create karna hi kaafi nahi. Server ko unauthorized access, malware, weak passwords aur doosray security risks se protect karna bhi zaroori hai.

## 2. What Is EC2 Hardening?

### Definition
EC2 hardening is the process of reducing security risks by securely configuring an EC2 instance, its operating system, network access, identities, and installed software.

### Roman Urdu Explanation
EC2 hardening ka matlab hai AWS ke EC2 server ko secure banana.

Jab hum naya server create karte hain, to uski security settings ko properly configure karna zaroori hota hai. Unnecessary services band karna, software update karna, access restrict karna aur logs monitor karna hardening ke important parts hain.

### Why Is EC2 Hardening Important?

- Unauthorized access ka risk kam hota hai.
- Server aur website ki security improve hoti hai.
- Malware aur vulnerabilities ke risk ko reduce karne mein help milti hai.
- Sensitive data ko protect karne mein help milti hai.
- Security monitoring aur incident investigation behtar hoti hai.
- Organization ki security requirements follow karne mein help milti hai.

### Real-Life Example
Agar aap apne ghar ka darwaza khula chhor dein, to koi bhi andar aa sakta hai.

Isi tarah agar EC2 server par SSH port sab ke liye open ho aur weak authentication use ho, to unauthorized log server tak pohanchne ki koshish kar sakte hain.

Server hardening ka maqsad unnecessary entry points ko band karna aur access ko control karna hai.

## 3. What Is the Attack Surface?

### Definition
The attack surface is the set of points through which an attacker could potentially access or affect a system.

### Roman Urdu Explanation
Attack surface se murad server ke woh tamam possible entry points hain jin ke zariye koi attacker system tak pohanchne ki koshish kar sakta hai.

Examples:

- Open network ports.
- Weak passwords.
- Unpatched software.
- Unnecessary running services.
- Exposed access keys.
- Incorrect file permissions.
- Publicly accessible administrative interfaces.

### How to Reduce the Attack Surface

1. Sirf required ports open karein.
2. Unnecessary software uninstall karein.
3. Unused services disable karein.
4. Operating system aur packages update rakhein.
5. Strong authentication use karein.
6. IAM permissions ko restrict karein.
7. Logs aur security alerts monitor karein.

## 4. What Is an EC2 Security Group?

### Definition
An AWS Security Group is a virtual firewall that controls inbound and outbound network traffic for supported AWS resources, including EC2 instances.

### Roman Urdu Explanation
Security Group AWS mein virtual firewall ka kaam karta hai. Is se hum decide karte hain ke EC2 instance par kis port se traffic aa sakta hai aur instance se kis tarah ka traffic bahar ja sakta hai.

### Common Ports

| Port | Service | Purpose |
|---|---|---|
| 22 | SSH | Linux server ka remote administration |
| 80 | HTTP | Website access |
| 443 | HTTPS | Secure website access |
| 3389 | RDP | Windows Remote Desktop |

### Security Group Best Practices

- SSH port 22 ko `0.0.0.0/0` se open na karein.
- SSH ke liye apne trusted IP address ko allow karein.
- Windows RDP port 3389 ko public internet ke liye open na karein.
- Sirf required web ports, jaise 80 aur 443, public karein.
- Database ports ko public access se protect karein.
- Unnecessary inbound rules remove karein.

### Example
Agar server sirf public website host kar raha hai, to aam tor par HTTP port 80 aur HTTPS port 443 ki inbound rules required ho sakti hain.

SSH ke liye port 22 ko sirf trusted administration source tak restrict karein.

Note: Agar AWS Systems Manager Session Manager configured hai, to server administration ke liye inbound SSH access ki zaroorat nahi bhi ho sakti.

## 5. What Is SSH?

### Definition
Secure Shell (SSH) is a network protocol used to securely access and administer remote computers.

### Roman Urdu Explanation
SSH aik secure protocol hai jis se hum apne computer se remote Linux server par login karke commands run kar sakte hain.

AWS EC2 mein SSH commonly port 22 use karta hai.

### Example Command

```bash
ssh -i my-key.pem ec2-user@YOUR-PUBLIC-IP
```

Is command mein:

- `ssh` remote server se secure connection establish karta hai.
- `-i my-key.pem` private key file specify karta hai.
- `ec2-user` Amazon Linux ke liye common default username hai.
- `YOUR-PUBLIC-IP` ki jagah apne EC2 instance ka actual public IP enter karein.

Important: Username AMI ke mutabiq different ho sakta hai. Private key ko kabhi GitHub par upload na karein.

## 6. Secure SSH Configuration

### Definition
SSH hardening means configuring SSH access to reduce unauthorized login attempts and unnecessary exposure.

### Roman Urdu Explanation
SSH hardening ka matlab SSH access ko secure banana hai. Is mein trusted sources se access allow karna, strong authentication use karna aur unnecessary login methods ko disable karna shamil ho sakta hai.

### Best Practices

1. SSH ko trusted IP addresses tak restrict karein.
2. Private key ko secure rakhein.
3. Root ke direct SSH login ko disable karne par ghour karein.
4. Password authentication ko disable karne se pehle key-based access verify karein.
5. SSH configuration change karne se pehle backup lein.
6. Existing session ko tab tak open rakhein jab tak new configuration test na ho jaye.
7. Production server par changes carefully karein.

### Check SSH Service

Amazon Linux par:

```bash
sudo systemctl status sshd
```

Yeh command SSH service ka status show karti hai.

### Check SSH Configuration

```bash
sudo sshd -t
```

Yeh SSH configuration ki syntax validate karti hai. Agar koi output nahi aata, to aam tor par syntax check successful hota hai.

Important: SSH configuration ko bina samjhe modify na karein. Ghalat settings se aap apne server se lock out ho sakti hain.

## 7. What Is a Key Pair?

### Definition
An AWS EC2 key pair consists of a public key and a private key used for supported secure authentication methods.

### Roman Urdu Explanation
EC2 key pair remote server se secure login karne ke liye use ho sakta hai.

- Public key server par configure hoti hai.
- Private key user ke paas secure rehti hai.

Private key ko kisi ke sath share nahi karna chahiye.

### Security Rules

- Private key ko secure location mein rakhein.
- GitHub repository mein private key upload na karein.
- Private key ko email ya public chat mein share na karein.
- Agar private key expose ho jaye, to affected access ko revoke ya replace karne ka plan banayein.

## 8. What Is OS Patching?

### Definition
Operating system patching is the process of applying software updates that fix bugs, improve stability, and address security vulnerabilities.

### Roman Urdu Explanation
Patching ka matlab operating system aur software ke updates install karna hai.

Software updates mein security fixes hoti hain jo known vulnerabilities ko address karti hain.

Agar server par purana software ho, to attacker known weakness ka faida uthane ki koshish kar sakta hai.

### Update Amazon Linux 2023

```bash
sudo dnf check-update
```

Yeh available updates check karta hai. Kuch package managers updates available hone par non-zero exit status bhi return kar sakte hain.

Packages update karne ke liye:

```bash
sudo dnf upgrade --refresh -y
```

### Update Ubuntu

```bash
sudo apt update
```

Yeh package lists update karta hai.

```bash
sudo apt upgrade -y
```

Yeh available package upgrades install karta hai.

Important: Commands apni operating system distribution ke mutabiq use karein. Production server par updates se pehle maintenance window aur backup/recovery plan consider karein.

## 9. What Is Least Privilege on a Server?

### Definition
Least privilege means granting users, applications, and services only the permissions necessary for their tasks.

### Roman Urdu Explanation
Server par har user ko administrator ya root access dena zaroori nahi hota.

Agar kisi user ko sirf website files read karni hain, to usay system ki tamam files modify karne ki permission dena security risk hai.

### Useful Linux Commands

Current user check karne ke liye:

```bash
whoami
```

Current user ki identity aur groups check karne ke liye:

```bash
id
```

Sudo permissions test karne ke liye:

```bash
sudo -l
```

Yeh current user ke liye available sudo permissions show kar sakta hai.

### Best Practices

- Daily tasks ke liye root account use na karein.
- Sudo access sirf required users ko dein.
- Shared accounts se avoid karein.
- User permissions ko regularly review karein.
- Unused user accounts disable ya remove karein.

## 10. What Is a Host Firewall?

### Definition
A host firewall is software running on a computer that controls network traffic according to configured rules.

### Roman Urdu Explanation
AWS Security Group cloud network level par traffic filter karta hai, jabke host firewall EC2 operating system ke andar traffic filter kar sakta hai.

Linux systems mein firewall tools distribution ke mutabiq different ho sakte hain.

### Important Difference

- Security Group: AWS resource ke network traffic ko control karta hai.
- Host Firewall: Operating system par traffic control karta hai.

Dono aik sath use ho sakte hain, lekin rules ko carefully coordinate karna zaroori hai.

### Ubuntu Firewall Check

```bash
sudo ufw status
```

Yeh Ubuntu par UFW firewall ka status show karta hai, agar UFW installed ho.

Important: Firewall enable ya modify karne se pehle required SSH access allow hone ki tasdeeq karein. Warna remote connection block ho sakta hai.

## 11. Disable Unnecessary Services

### Definition
Service hardening involves disabling or removing services that are not required for the server's intended function.

### Roman Urdu Explanation
Agar server par unnecessary services chal rahi hon, to woh additional attack surface create kar sakti hain.

Is liye sirf required services run karni chahiye.

### List Running Services

```bash
systemctl --type=service --state=running
```

Yeh running services ki list show karta hai.

### Check Listening Ports

```bash
sudo ss -lntup
```

Yeh listening network sockets aur unse related processes ki information show kar sakta hai.

### Important Safety Rule
Kisi service ko disable karne se pehle samjhein ke woh kya kaam karti hai. Production server par required service disable karne se website ya application band ho sakti hai.

## 12. What Is File Permission Hardening?

### Definition
File permission hardening means assigning appropriate read, write, and execute permissions to files and directories.

### Roman Urdu Explanation
Linux mein file permissions decide karti hain ke owner, group aur doosray users kisi file ko read, write ya execute kar sakte hain ya nahi.

Agar sensitive file har user ke liye readable ya writable ho, to data exposure ya unauthorized changes ka risk barh sakta hai.

### View File Permissions

```bash
ls -l
```

Yeh files aur directories ki permissions show karta hai.

### Example: Restrict a Private File

```bash
chmod 600 private-file.txt
```

Yeh owner ko read/write permission aur doosray users ko koi permission nahi deta.

Important: Yeh example sirf us file ke liye use karein jiske liye aisi permissions suitable hon. Har file par blindly `chmod 600` apply na karein.

### Avoid Unnecessary World-Writable Permissions

Sensitive files aur directories ko unnecessary world-writable na banayein. Permissions change karne se pehle application ki requirements verify karein.

## 13. What Is IAM Role for EC2?

### Definition
An IAM role for EC2 allows applications running on an instance to obtain temporary AWS credentials for authorized operations.

### Roman Urdu Explanation
Agar EC2 instance ko S3, CloudWatch ya kisi doosri AWS service ke sath interact karna hai, to IAM role use kiya ja sakta hai.

Is se application ke code mein permanent access keys store karne ki zaroorat kam hoti hai.

### Example
Agar application ko S3 bucket se sirf files read karni hain, to EC2 role ko sirf required bucket aur read actions ki permission dein.

### Best Practices

- Har application ko required permissions tak limit karein.
- AdministratorAccess jaisi broad policy unnecessary use na karein.
- Application ke andar access keys hard-code na karein.
- Role permissions ko regularly review karein.

## 14. What Is Data Encryption?

### Definition
Encryption transforms readable data into a protected form that can only be read by parties with the appropriate decryption capability.

### Roman Urdu Explanation
Encryption data ko aisi form mein convert karti hai jise correct key ya decryption method ke baghair read karna mushkil hota hai.

Server security mein encryption do important jagahon par use hoti hai:

**1. Encryption at Rest**

Jab data disk ya storage mein saved ho, usay encrypt karna.

Example: EC2 EBS volumes ko encryption ke sath configure karna.

**2. Encryption in Transit**

Jab data network par transfer ho raha ho, usay encrypt karna.

Example: Website par HTTPS/TLS use karna.

### Best Practices

- Sensitive EBS volumes ko encrypt karein.
- Application ki requirements ke mutabiq HTTPS use karein.
- Encryption keys ko securely manage karein.
- Sensitive data aur credentials ko logs mein expose na karein.

## 15. What Is EBS Encryption?

### Definition
Amazon Elastic Block Store (EBS) encryption protects data stored on supported EBS volumes and helps protect data during supported transfers between an instance and its attached volume.

### Roman Urdu Explanation
EBS woh storage service hai jo EC2 instances ke sath block storage provide karti hai.

EBS encryption se disk par stored data ki confidentiality improve hoti hai. Encryption ko volume create karte waqt configure kiya ja sakta hai, aur AWS KMS keys use ho sakti hain.

### Security Benefits

- Stored data encryption.
- Supported snapshots ki encryption.
- Data confidentiality improve karna.
- Security aur compliance requirements ko support karna.

Important: Encryption access permissions ka replacement nahi hai. IAM, key policies aur operating system access ko bhi secure rakhna zaroori hai.

## 16. What Is Logging and Monitoring?

### Definition
Logging records system and application events, while monitoring observes system health, performance, and security-related activity.

### Roman Urdu Explanation
Logs server par hone wale events ka record rakhte hain. Monitoring se hum server ki health, resource usage aur possible security issues ko observe kar sakte hain.

### Examples of Logs

- SSH login events.
- Operating system events.
- Apache/Nginx access logs.
- Application errors.
- Security-related events.

### Useful Linux Commands

System journal ki recent entries dekhne ke liye:

```bash
sudo journalctl -n 50
```

SSH service ke logs dekhne ke liye, supported Linux systems par:

```bash
sudo journalctl -u sshd -n 50
```

Note: Kuch systems par SSH service ka naam `ssh` ho sakta hai.

### AWS Monitoring Tools

**Amazon CloudWatch**

Metrics, logs aur alarms ke zariye monitoring provide karta hai.

**AWS CloudTrail**

AWS account mein supported API activity ka record provide karta hai.

**Amazon GuardDuty**

Supported AWS data sources aur threat intelligence ke zariye potential threats identify karne mein help karta hai.

Yeh services apni configuration, permissions aur supported features ke mutabiq kaam karti hain.

## 17. What Is AWS Systems Manager Session Manager?

### Definition
AWS Systems Manager Session Manager provides managed access to supported EC2 instances without requiring inbound SSH or RDP ports.

### Roman Urdu Explanation
Session Manager ke zariye authorized users AWS Console ya supported tools se instance par shell session open kar sakte hain.

Agar Session Manager properly configured ho, to remote administration ke liye public SSH port open karne ki zaroorat nahi bhi ho sakti.

### Benefits

- Inbound SSH access ki dependency kam ho sakti hai.
- IAM ke zariye access control kiya ja sakta hai.
- Centralized access management mein help milti hai.
- Configured hone par session activity logging support ho sakti hai.

### Requirements
Instance, IAM permissions, Systems Manager agent aur required network connectivity ko service requirements ke mutabiq configure karna hota hai.

## 18. What Is AWS Inspector?

### Definition
Amazon Inspector is a vulnerability management service that helps discover software vulnerabilities and unintended network exposure in supported AWS workloads.

### Roman Urdu Explanation
Amazon Inspector supported workloads mein known software vulnerabilities aur kuch network exposure risks identify karne mein help karta hai.

Security team findings review karke vulnerabilities ko prioritize aur remediate kar sakti hai.

### Example
Agar kisi supported EC2 workload mein vulnerable software version detect ho, to finding ko review karke approved patching process follow kiya ja sakta hai.

Important: Vulnerability scanning hardening ka replacement nahi. Updates, access controls aur monitoring phir bhi zaroori hain.

## 19. Practical Lab — Basic EC2 Hardening

### Lab Objective
Is lab mein hum EC2 instance ki basic security review aur hardening practices apply karenge.

### Step 1: Review the Security Group

1. AWS Console mein EC2 open karein.
2. Apna test instance select karein.
3. Security tab open karein.
4. Associated Security Group par click karein.
5. Inbound rules review karein.
6. Unnecessary ports remove karein.
7. SSH ko trusted IP tak restrict karein, agar SSH required ho.
8. Public website ke liye sirf required web ports allow karein.

### Step 2: Connect Securely

Authorized SSH ya configured Systems Manager Session Manager use karein.

SSH example:

```bash
ssh -i my-key.pem ec2-user@YOUR-PUBLIC-IP
```

`my-key.pem`, username aur public IP ko apni actual configuration ke mutabiq replace karein.

### Step 3: Identify the Operating System

```bash
cat /etc/os-release
```

Yeh operating system ki information show karta hai.

### Step 4: Review Available Updates

Amazon Linux 2023:

```bash
sudo dnf check-update
```

Ubuntu:

```bash
sudo apt update
```

Operating system ke mutabiq appropriate update process follow karein.

### Step 5: Review Running Services

```bash
systemctl --type=service --state=running
```

Unnecessary services ko identify karein. Disable karne se pehle unki purpose aur dependencies verify karein.

### Step 6: Review Listening Ports

```bash
sudo ss -lntup
```

Dekhein ke kaun se ports listening state mein hain. Har listening port public internet se accessible nahi hota; network rules bhi matter karte hain.

### Step 7: Review User Permissions

```bash
whoami
```

```bash
id
```

```bash
sudo -l
```

Yeh commands current identity aur available sudo permissions ko review karne mein help karti hain.

### Step 8: Review Disk Encryption

AWS EC2 Console mein instance ke attached EBS volumes open karein.

Volume details mein encryption status verify karein. Existing unencrypted volumes ko encrypt karne ke liye planned migration ya supported conversion process ki zaroorat ho sakti hai.

### Step 9: Review Logs

```bash
sudo journalctl -n 50
```

Application logs aur relevant authentication logs ko bhi review karein.

### Step 10: Document the Changes

Lab ke end par record karein:

- Kaun se ports allowed hain.
- Kaun se updates apply kiye gaye.
- Kaun si services required hain.
- Instance ka access method kya hai.
- Monitoring aur logging configured hain ya nahi.

## 20. Common EC2 Security Mistakes

### Mistake 1: SSH Open to Everyone
Port 22 ko `0.0.0.0/0` se open karne se server public internet se SSH attempts receive kar sakta hai.

### Mistake 2: Using Administrator Permissions Everywhere
Har user ya application ko broad permissions dena unnecessary risk create karta hai.

### Mistake 3: Ignoring Updates
Outdated operating systems aur packages known vulnerabilities ke liye exposed reh sakte hain.

### Mistake 4: Storing Access Keys in Code
Source code mein permanent credentials rakhne se keys leak ho sakti hain.

### Mistake 5: Disabling Security Tools
Logs, monitoring ya host firewall ko bina proper review disable karna security visibility ko kam kar sakta hai.

### Mistake 6: No Backup or Recovery Plan
Hardening ke dauran ghalat configuration ya software update se service interrupt ho sakti hai. Recovery plan aur suitable backups important hain.

## 21. EC2 Hardening Checklist

- [ ] Security Group rules review kiye.
- [ ] SSH/RDP access ko restrict kiya.
- [ ] Required operating system updates apply kiye.
- [ ] Unnecessary services review ki.
- [ ] User aur sudo permissions review ki.
- [ ] IAM role ko least privilege ke mutabiq configure kiya.
- [ ] EBS encryption status check kiya.
- [ ] HTTPS/TLS requirements review ki.
- [ ] Logs aur monitoring configure ki.
- [ ] AWS credentials ko secure rakha.
- [ ] Backup aur recovery plan review kiya.
- [ ] Security changes document kiye.

## 22. Important Interview Questions

### Q1. What is EC2 hardening?
EC2 hardening is the process of securely configuring an EC2 instance to reduce security risks.

### Q2. What is an attack surface?
An attack surface is the set of possible points through which a system may be accessed or affected.

### Q3. What is a Security Group?
A Security Group is an AWS virtual firewall that controls inbound and outbound traffic.

### Q4. Why should SSH access be restricted?
Restricting SSH access reduces exposure to unauthorized connection attempts.

### Q5. What is SSH?
SSH is a protocol used to securely administer remote systems.

### Q6. What is OS patching?
OS patching means applying updates that fix bugs and address security vulnerabilities.

### Q7. What is least privilege?
Least privilege means giving users and applications only the permissions needed for their tasks.

### Q8. What is EBS encryption?
EBS encryption protects data stored on supported EBS volumes.

### Q9. What is the difference between a Security Group and a host firewall?
A Security Group filters traffic at the AWS resource networking level, while a host firewall filters traffic inside the operating system.

### Q10. What is CloudTrail?
AWS CloudTrail records supported AWS account activity and API events.

### Q11. What is Amazon Inspector?
Amazon Inspector helps identify vulnerabilities and certain unintended network exposure in supported workloads.

### Q12. What is Session Manager?
Session Manager provides managed access to supported instances without requiring inbound SSH or RDP ports.

## 23. Class Summary

- EC2 is AWS ki virtual server service hai.
- Hardening ka maqsad server ke security risks ko reduce karna hai.
- Security Groups inbound aur outbound network traffic control karte hain.
- SSH access ko trusted sources tak restrict karna chahiye.
- OS patching known vulnerabilities ko address karne mein help karti hai.
- Least privilege se unnecessary permissions kam hoti hain.
- Unnecessary services aur open ports review karne chahiye.
- File permissions ko secure rakhna zaroori hai.
- EC2 IAM roles applications ko controlled AWS access dete hain.
- EBS encryption stored data ko protect karne mein help karti hai.
- Logs aur monitoring security events identify karne mein help karte hain.
- Session Manager inbound SSH access ki zaroorat ko kam kar sakta hai.
- Regular security review aur recovery planning EC2 hardening ke important parts hain.
