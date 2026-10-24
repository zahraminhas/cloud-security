
# Class 7 — Servers, Apache vs Nginx, Ports & Security Groups, Hosting Lab

## 1. What Is a Server?

### Definition
A server is a computer or software that provides services, resources, or data to other computers called clients over a network.

### Roman Urdu Explanation
Server aik computer ya software hota hai jo network ke zariye doosray computers ko data, files, websites ya doosri services provide karta hai.

Jab hum browser mein kisi website ka address enter karte hain, to hamara browser server se website ka data request karta hai. Server request receive karke response send karta hai.

### Real-Life Example
Jab aap browser mein `www.google.com` open karti hain:
1. Aapka browser website ki request send karta hai.
2. Google ka server request receive karta hai.
3. Server website ka data send karta hai.
4. Browser website ko screen par display karta hai.

### Types of Servers

**1. Web Server:** Website ke pages aur files serve karta hai.

**2. File Server:** Network par files store aur share karta hai.

**3. Database Server:** Data ko store, organize aur retrieve karta hai.

**4. Mail Server:** Emails send aur receive karne mein help karta hai.

**5. Application Server:** Applications ko run karne ke liye services provide karta hai.

**6. DNS Server:** Domain name ko IP address ke sath resolve karne mein help karta hai.

## 2. What Is a Web Server?

### Definition
A web server is software, and sometimes the computer running it, that receives HTTP/HTTPS requests and delivers web content to clients.

### Roman Urdu Explanation
Web server aik software hota hai jo browser ki HTTP ya HTTPS request receive karta hai aur website ka content, jaise HTML, CSS, JavaScript aur images, browser ko send karta hai.

Web server ki common examples Apache aur Nginx hain.

### How a Web Server Works

1. User browser mein website ka URL enter karta hai.
2. Browser server ke IP address se connection establish karta hai.
3. Browser HTTP ya HTTPS request send karta hai.
4. Web server request process karta hai.
5. Server response mein website ka content send karta hai.
6. Browser content ko display karta hai.

## 3. What Is Apache?

### Definition
Apache HTTP Server is an open-source web server software used to serve websites and web applications over HTTP and HTTPS.

### Roman Urdu Explanation
Apache aik popular aur open-source web server hai. Iska use websites ko internet ya private network par available karwane ke liye hota hai.

Apache configuration files ke zariye website ki settings manage ki ja sakti hain. Is mein `.htaccess` file bhi use ki ja sakti hai, agar server configuration allow karti ho.

### Features of Apache

- Open-source software.
- HTTP aur HTTPS support karta hai.
- `.htaccess` ke zariye directory-level configuration possible hai, jab enabled ho.
- Modules ke zariye additional features add kiye ja sakte hain.
- Linux aur Windows samait multiple operating systems par available hai.
- Dynamic websites ke sath use ho sakta hai.

### Apache Example
Agar aap apni website ke pages server par rakhna chahti hain, to Apache un pages ko browser ki requests ke jawab mein deliver kar sakta hai.

## 4. What Is Nginx?

### Definition
Nginx is an open-source web server that can also act as a reverse proxy, load balancer, and HTTP cache.

### Roman Urdu Explanation
Nginx aik web server hai jo websites ka content serve kar sakta hai. Isay reverse proxy aur load balancer ke taur par bhi use kiya jata hai.

Nginx bohat si simultaneous connections ko efficiently handle karne ke liye mashhoor hai.

### Features of Nginx

- Open-source software.
- HTTP aur HTTPS support karta hai.
- Static files efficiently serve kar sakta hai.
- Reverse proxy ke taur par kaam karta hai.
- Load balancing support karta hai.
- Multiple connections handle karne ke liye event-driven architecture use karta hai.

### What Is a Reverse Proxy?

Reverse proxy aik server hota hai jo clients ki requests receive karta hai aur unhein backend servers tak forward karta hai.

Roman Urdu: User ki request pehle reverse proxy tak aati hai. Phir reverse proxy request ko munasib backend server tak bhejta hai aur response user tak pohanchata hai.

## 5. Apache vs Nginx

| Feature | Apache | Nginx |
|---|---|---|
| Type | Web server | Web server and reverse proxy |
| Architecture | Process/thread-based models support karta hai | Event-driven architecture use karta hai |
| Static Files | Static content serve karta hai | Static content efficiently serve karta hai |
| Configuration | `.htaccess` support kar sakta hai | `.htaccess` use nahi karta |
| Reverse Proxy | Support karta hai | Commonly use hota hai |
| Load Balancing | Available through modules and configurations | Built-in load-balancing capabilities |
| Best Use | Flexible configurations aur compatible applications | High concurrent connections aur reverse proxy setups |

### Which One Should We Choose?

Apache tab useful ho sakta hai jab aapko `.htaccess` ya Apache-specific configuration ki zaroorat ho.

Nginx tab useful ho sakta hai jab aap reverse proxy, load balancing ya bohat si simultaneous connections handle karna chahti hon.

Dono web servers powerful hain. Best choice project ki requirements aur configuration par depend karti hai.

## 6. What Is a Port?

### Definition
A port is a logical communication endpoint used by network applications to send and receive data.

### Roman Urdu Explanation
IP address computer ya server ko network par identify karta hai, jabke port number us computer par specific service ya application tak communication pohanchane mein help karta hai.

Example: Aik server par website, SSH aur database service chal sakti hain. Har service apne configured port par requests receive kar sakti hai.

Port numbers 0 se 65535 tak hote hain.

### Common Network Ports

| Port | Protocol/Service | Purpose |
|---|---|---|
| 20/21 | FTP | File transfer |
| 22 | SSH | Secure remote login |
| 25 | SMTP | Email transfer |
| 53 | DNS | Domain name resolution |
| 80 | HTTP | Web traffic without TLS |
| 443 | HTTPS | Encrypted web traffic using TLS |
| 3306 | MySQL | MySQL database connections |
| 5432 | PostgreSQL | PostgreSQL database connections |
| 3389 | RDP | Remote Desktop Protocol |

Note: Services can be configured to use different ports. A port number alone does not guarantee that a service is running.

## 7. What Is HTTP and HTTPS?

### HTTP Definition
HTTP stands for Hypertext Transfer Protocol. It is used for communication between web clients and servers.

Roman Urdu: HTTP browser aur web server ke darmiyan website data exchange karne ke liye use hota hai.

### HTTPS Definition
HTTPS is HTTP secured using TLS encryption.

Roman Urdu: HTTPS browser aur server ke darmiyan data ko encrypt karta hai, jis se network par data ko read ya modify karna mushkil hota hai.

### Difference

- HTTP commonly uses port 80.
- HTTPS commonly uses port 443.
- HTTPS helps protect data in transit.
- Sensitive information ke liye HTTPS use karna chahiye.

## 8. What Is a Security Group in AWS?

### Definition
An AWS security group is a virtual firewall that controls inbound and outbound traffic for supported AWS resources, such as EC2 instances.

### Roman Urdu Explanation
AWS Security Group aik virtual firewall hai. Iska kaam decide karna hai ke EC2 instance tak kis qisam ka network traffic aa sakta hai aur instance se kis qisam ka traffic bahar ja sakta hai.

Security Group ke rules mein protocol, port range aur source ya destination define kiya jata hai.

### Inbound Rules
Inbound rules control incoming traffic.

Example:
- SSH (port 22): Remote administration.
- HTTP (port 80): Website access.
- HTTPS (port 443): Secure website access.

### Outbound Rules
Outbound rules control outgoing traffic from the resource.

Example:
- EC2 instance ko software updates download karne ke liye internet access ki zaroorat ho sakti hai.
- Application ko database ya doosri services se connect karna ho sakta hai.

### Important Security Group Facts

1. Security Groups are stateful. Allowed incoming connections ke responses automatically allow ho jate hain.
2. Rules allow traffic; Security Groups mein explicit deny rules define nahi kiye jate.
3. Multiple Security Groups aik supported resource ke sath associate ho sakte hain.
4. SSH port 22 ko `0.0.0.0/0` se open karna security risk hai.
5. Sirf required ports allow karein.
6. SSH ke liye apne trusted IP address ko allow karna behtar hai.
7. Database ports ko public internet ke liye open na karein jab tak koi justified requirement na ho.

## 9. What Is Amazon EC2?

### Definition
Amazon Elastic Compute Cloud (Amazon EC2) is an AWS service that provides virtual servers called instances.

### Roman Urdu Explanation
Amazon EC2 AWS ki service hai jis se hum cloud mein virtual server create kar sakte hain. Hum operating system choose kar sakte hain, software install kar sakte hain aur apni website host kar sakte hain.

### EC2 Can Be Used For

- Hosting websites.
- Running web applications.
- Testing software.
- Running backend services.
- Learning Linux and server administration.

### Basic EC2 Requirements

- An AWS account.
- An EC2 instance.
- A suitable operating system image (AMI).
- A key pair or another configured secure access method.
- A security group.
- A public IP address or another network access method, if external access is required.

## 10. Hosting Lab — Host a Website on an EC2 Instance

### Lab Objective
Is lab ka maqsad AWS EC2 instance par aik simple website host karna aur browser mein usay access karna hai.

### Step 1: Launch an EC2 Instance

1. AWS Management Console open karein.
2. EC2 service select karein.
3. Launch Instance par click karein.
4. Instance ka naam `Web-Server-Lab` rakh dein.
5. Amazon Linux jaisi supported AMI select karein.
6. Learning ke liye suitable instance type choose karein.
7. Key pair create ya select karein.
8. Security Group configure karein.
9. Instance launch karein.

Important: AWS account par charges apply ho sakte hain. Current pricing aur Free Tier eligibility check karein.

### Step 2: Configure the Security Group

Inbound rules mein required access allow karein:

| Type | Port | Source | Purpose |
|---|---|---|---|
| SSH | 22 | My IP | Secure server administration |
| HTTP | 80 | 0.0.0.0/0 | Public website access |

Agar IPv6 se bhi website accessible karni ho to appropriate IPv6 rule separately configure karna hoga.

SSH ko `0.0.0.0/0` se open na karein. Public website ke liye HTTP ko public allow karna normal ho sakta hai, lekin SSH ko restricted rakhna chahiye.

### Step 3: Connect to the EC2 Instance

AWS Console mein EC2 instance select karein aur Connect option use karein. Agar EC2 Instance Connect available aur configured hai to browser-based connection use ki ja sakti hai.

Successful connection ke baad aap terminal mein Linux commands run kar sakti hain.

### Step 4: Update the System

Amazon Linux 2023 par package information aur installed packages update karne ke liye:

```bash
sudo dnf update -y
```

Roman Urdu: `sudo` administrative permissions ke sath command run karta hai. `dnf update` system packages ko update karta hai.

### Step 5: Install Apache

Amazon Linux 2023 par Apache install karne ke liye:

```bash
sudo dnf install httpd -y
```

Roman Urdu: Yeh command Apache HTTP Server package install karti hai.

Note: Doosri Linux distributions par package manager aur package name different ho sakte hain.

### Step 6: Start Apache

```bash
sudo systemctl enable --now httpd
```

Roman Urdu:
- `systemctl` system services manage karta hai.
- `enable` service ko boot par start hone ke liye configure karta hai.
- `--now` service ko abhi bhi start karta hai.

### Step 7: Check Apache Status

```bash
sudo systemctl status httpd
```

Agar service successfully run ho rahi ho to output mein `active (running)` nazar aa sakta hai.

Status screen se exit karne ke liye `q` press karein.

### Step 8: Create a Simple Web Page

```bash
echo '<html><head><title>My Web Server</title></head><body><h1>Welcome to My AWS Website</h1><p>My first hosting lab is successful.</p></body></html>' | sudo tee /var/www/html/index.html
```

Roman Urdu: Yeh command aik simple HTML page create karti hai jo Apache ke default web directory mein save hota hai.

### Step 9: Test Apache Locally

EC2 terminal mein run karein:

```bash
curl http://localhost
```

Agar HTML content output mein aa jaye to Apache local machine par response de raha hai.

### Step 10: Open the Website in a Browser

1. AWS Console mein EC2 instance details open karein.
2. Instance ka public IPv4 address copy karein.
3. Browser mein yeh address enter karein:

```text
http://YOUR-PUBLIC-IP
```

`YOUR-PUBLIC-IP` ko apne actual public IPv4 address se replace karein.

Agar security group mein HTTP port 80 allowed hai, instance ke paas suitable network route aur public address hai, aur Apache running hai, to website browser mein open ho sakti hai.

### Step 11: Troubleshooting

Agar website open nahi ho rahi to yeh cheezein check karein:

**1. Apache service**

```bash
sudo systemctl status httpd
```

**2. Local HTTP response**

```bash
curl -I http://localhost
```

**3. Listening ports**

```bash
sudo ss -lntp
```

**4. Security Group**
Confirm karein ke inbound HTTP port 80 allowed hai.

**5. Network configuration**
Check karein ke instance ke paas public IP, suitable subnet route aur internet gateway connectivity ho, agar public access required hai.

**6. Operating system firewall**
Check karein ke operating system firewall HTTP traffic ko block na kar raha ho.

**7. Public IP**
Confirm karein ke browser mein correct public IPv4 address use ho raha hai.

## 11. Basic Linux Commands for Hosting

### Check Current User

```bash
whoami
```

Yeh current logged-in user ka naam show karta hai.

### Check Server IP Information

```bash
ip addr
```

Yeh network interfaces aur unke IP addresses ki information show karta hai.

### Check Running Processes

```bash
ps aux
```

Yeh running processes ki list show karta hai.

### Check Disk Space

```bash
df -h
```

Yeh file systems ki disk usage readable format mein show karta hai.

### View Apache Logs

```bash
sudo tail -n 50 /var/log/httpd/access_log
```

Yeh Apache ke access log ki last 50 lines show karta hai.

```bash
sudo tail -n 50 /var/log/httpd/error_log
```

Yeh Apache ke error log ki last 50 lines show karta hai.

## 12. Basic Security Best Practices

1. Sirf required ports open karein.
2. SSH access ko trusted IP addresses tak restrict karein.
3. Root account ko routine work ke liye use na karein.
4. System packages aur web server ko updated rakhein.
5. Website par HTTPS configure karein jab production use ho.
6. Credentials aur private keys ko secure rakhein.
7. Logs ko regularly review karein.
8. AWS credentials ko GitHub repository mein upload na karein.
9. Website ki files aur permissions ko properly configure karein.
10. Lab complete hone ke baad unnecessary AWS resources terminate karein, taake unwanted charges se bacha ja sake.

## 13. Important Interview Questions

### Q1. What is a server?
A server is a computer or software that provides services or resources to clients over a network.

### Q2. What is Apache?
Apache is an open-source web server used to serve websites and web applications.

### Q3. What is Nginx?
Nginx is an open-source web server that can also work as a reverse proxy and load balancer.

### Q4. What is the difference between Apache and Nginx?
Apache supports flexible configuration, including `.htaccess` when enabled. Nginx uses an event-driven architecture and is widely used for static content, reverse proxying and load balancing.

### Q5. What is a port?
A port is a logical communication endpoint used by network applications.

### Q6. Which port is commonly used by HTTP?
HTTP commonly uses port 80.

### Q7. Which port is commonly used by HTTPS?
HTTPS commonly uses port 443.

### Q8. What is an AWS Security Group?
It is a virtual firewall that controls inbound and outbound traffic for supported AWS resources.

### Q9. What is Amazon EC2?
Amazon EC2 is an AWS service that provides virtual servers called instances.

### Q10. Which command installs Apache on Amazon Linux 2023?
```bash
sudo dnf install httpd -y
```

### Q11. Which command starts Apache and enables it at boot?
```bash
sudo systemctl enable --now httpd
```

### Q12. Why should SSH port 22 not be open to everyone?
Because unrestricted SSH access increases the risk of unauthorized login attempts.

## 14. Class Summary

- Server clients ko services aur resources provide karta hai.
- Web server HTTP/HTTPS requests receive karke website content deliver karta hai.
- Apache aur Nginx popular web servers hain.
- Port numbers network services tak communication pohanchane mein help karte hain.
- HTTP commonly port 80 aur HTTPS port 443 use karta hai.
- AWS Security Groups virtual firewalls hain.
- Amazon EC2 cloud mein virtual servers provide karta hai.
- Apache install aur configure karke EC2 par simple website host ki ja sakti hai.
- Secure hosting ke liye minimum required ports allow karna aur SSH access restrict karna zaroori hai.
