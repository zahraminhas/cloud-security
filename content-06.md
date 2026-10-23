
# Class 6 - EBS, Networking, Key Pair, User Data, EC2, Lifecycle, Pricing & Scaling

## 1. Amazon EC2 (Elastic Compute Cloud)

### Definition
Amazon EC2 is an AWS service that provides virtual servers in the cloud.

### EC2 Kya Hai?
Amazon EC2 AWS ki aik important service hai jis ki madad se hum internet ke zariye virtual computer ya server bana sakte hain. Is server ko hum apni zaroorat ke mutabiq use kar sakte hain.

Misal ke taur par, agar hum koi website ya application banana chahein aur usay internet par chalana chahein, to hum EC2 par aik virtual server launch kar sakte hain.

EC2 mein hum apni zaroorat ke mutabiq CPU, RAM, storage aur operating system select kar sakte hain.

### EC2 Kaise Kaam Karta Hai?
1. Sab se pehle AWS account mein login karte hain.
2. EC2 service open karte hain.
3. Apni zaroorat ke mutabiq Amazon Machine Image (AMI) select karte hain.
4. Instance type select karte hain.
5. Networking aur security settings configure karte hain.
6. Launch Instance par click karte hain.
7. Instance running state mein aa jaye to usay apne kaam ke liye use kar sakte hain.

### Important Terms

- **Instance:** Cloud mein aik virtual server ko instance kehte hain.
- **AMI:** Amazon Machine Image aik template hoti hai jis mein operating system aur launch ke liye zaroori configuration hoti hai.
- **Instance Type:** Ye decide karta hai ke server ko kitna CPU, RAM aur doosre computing resources milenge.
- **Launch:** Naya EC2 instance create aur start karne ke process ko launch kehte hain.

### EC2 Ke Benefits
- Hum jaldi virtual server bana sakte hain.
- Zaroorat ke mutabiq computing capacity select kar sakte hain.
- Linux aur Windows jaise operating systems use kar sakte hain.
- Workload ke mutabiq resources increase ya decrease kar sakte hain.
- Different pricing options mein se apne liye suitable option choose kar sakte hain.

### Real-Life Example
EC2 ko aik rented computer samjhein jo aap apne ghar mein rakhne ke bajaye AWS ke data center mein use kar rahi hain.

---

## 2. Amazon EBS (Elastic Block Store)

### Definition
Amazon EBS is a block storage service that provides persistent storage volumes for EC2 instances.

### EBS Kya Hai?
Amazon EBS AWS ki storage service hai. Ye EC2 instance ke saath hard drive ki tarah kaam karti hai.

Jis tarah normal computer mein hard drive ya SSD par files, software aur operating system store hota hai, isi tarah EBS volume mein bhi data store kiya ja sakta hai.

EBS ka data aam tor par EC2 instance stop ya reboot karne ke baad bhi rehta hai.

### EBS Kaise Kaam Karta Hai?
1. AWS Console mein EC2 open karte hain.
2. EBS volume create karte hain.
3. Volume ke liye size aur doosri settings select karte hain.
4. Volume ko compatible EC2 instance ke saath attach karte hain.
5. Operating system mein volume ko zaroorat ke mutabiq format aur mount karte hain.
6. Ab is storage par data save kiya ja sakta hai.

### EBS Ki Important Features

- **Persistent Storage:** Instance stop hone ke baad bhi volume ka data aam tor par rehta hai.
- **Snapshots:** EBS volume ka backup banane mein madad dete hain.
- **Volume Size:** Zaroorat ke mutabiq storage size select kar sakte hain.
- **Detach and Attach:** Compatible volume ko aik instance se detach karke doosre compatible instance ke saath attach kiya ja sakta hai.
- **Availability Zone:** EBS volume aik specific Availability Zone mein hota hai.

### EBS Snapshot Kya Hai?
EBS Snapshot aik point-in-time backup hota hai jo volume ke data ko recover karne mein madad kar sakta hai.

Agar data delete ya corrupt ho jaye, to snapshot se naya volume create karke recovery ki ja sakti hai.

### EBS Aur EC2 Mein Farq
- EC2 computing aur processing ke liye virtual server provide karta hai.
- EBS data store karne ke liye storage provide karta hai.

### Real-Life Example
EC2 ko computer aur EBS ko us computer ki hard drive samjhein.

---

## 3. EC2 Networking

### Definition
EC2 networking allows EC2 instances to communicate with other AWS resources and the internet.

### Networking Kya Hai?
Networking ka matlab computers aur servers ko aapas mein connect karna hai taake woh data send aur receive kar saken.

EC2 networking ki madad se hum apne virtual server ko doosre AWS resources, internet aur users ke saath communicate karne ke qabil banate hain.

### 3.1 VPC (Virtual Private Cloud)

VPC AWS ke andar aik logically isolated virtual network hota hai.

Hum VPC ke andar apne resources ko organize kar sakte hain aur network configuration manage kar sakte hain.

### 3.2 Subnet

Subnet VPC ke IP address range ka aik hissa hota hai.

Subnet ki madad se hum VPC ke resources ko different network sections mein divide kar sakte hain.

Public subnet ya private subnet ka practical internet access uski routing aur doosri network settings par depend karta hai.

### 3.3 IP Address

IP address network par kisi device ya interface ko identify karne ke liye use hota hai.

- **Private IP:** VPC ke andar internal communication ke liye use hota hai.
- **Public IP:** Required configuration ke saath internet se communication mein madad deta hai.

### 3.4 Security Group

Security Group EC2 instance ke liye virtual firewall ka kaam karta hai.

Ye rules ke mutabiq network traffic control karta hai.

Misal:
- HTTP traffic ke liye port 80 allow karna.
- HTTPS traffic ke liye port 443 allow karna.
- SSH ke liye port 22 sirf trusted IP address se allow karna.

Security Group mein unnecessary ports ya tamam IP addresses ke liye SSH access open karne se bachna chahiye.

### 3.5 Internet Gateway

Internet Gateway VPC aur internet ke darmiyan communication enable karta hai jab required routes aur public IP configuration mojood hon.

### 3.6 Route Table

Route Table network traffic ke liye rasta decide karti hai.

Ye batati hai ke traffic ko destination tak pohanchne ke liye kis route ya gateway ki taraf bhejna hai.

### Networking Ka Real-Life Example
VPC ko aik society samjhein, subnet ko society ke different blocks, IP address ko ghar ka address aur Security Group ko security guard ke rules samjhein.

---

## 4. EC2 Key Pair

### Definition
An EC2 key pair consists of a public key and a private key used for secure authentication.

### Key Pair Kya Hai?
EC2 Key Pair server par securely login karne ke liye use hota hai.

Is mein do keys hoti hain:

### 4.1 Public Key
Public key ko AWS instance par configure kiya jata hai. Ye authentication process mein madad karti hai.

### 4.2 Private Key
Private key user ke paas securely rehti hai. Linux EC2 instance par SSH ke zariye login karne ke liye isay use kiya ja sakta hai.

### Key Pair Kaise Kaam Karta Hai?
1. EC2 instance launch karte waqt key pair select karte hain.
2. AWS public key ko instance par configure karta hai.
3. User apni private key ko secure rakhta hai.
4. SSH client private key use karke login ki koshish karta hai.
5. Agar authentication aur doosri security settings sahi hon, to login ho sakta hai.

### Key Pair Ki Importance
- Secure authentication mein madad karta hai.
- Linux instances par SSH access ke liye use hota hai.
- Private key ko secret rakhna zaroori hai.
- Private key ko public website ya GitHub repository par upload nahi karna chahiye.

### Real-Life Example
Key Pair ko lock aur uski chaabi ki misaal se samjhein. Public key server par hoti hai, jabke private key aap ke paas securely rehti hai.

Important: Agar private key kho jaye, to usi key ko dobara download karna aam tor par mumkin nahi hota. Access recover karne ke liye doosre authorized methods ki zaroorat ho sakti hai.

---

## 5. EC2 User Data

### Definition
EC2 User Data allows users to provide startup scripts or commands to an EC2 instance.

### User Data Kya Hai?
User Data EC2 ki aik feature hai jis ki madad se hum server launch karte waqt startup commands ya scripts provide kar sakte hain.

Is ka faida ye hai ke hum software manually install karne ke bajaye initial setup ko automate kar sakte hain.

### User Data Ke Uses
- Web server install karna.
- Software installation automate karna.
- Initial configuration karna.
- Startup par commands run karna.
- Website ki basic files create karna.

### User Data Ka Example

```bash
#!/bin/bash
dnf install -y httpd
systemctl enable --now httpd
echo "Welcome to AWS EC2" > /var/www/html/index.html
```

### Commands Ki Explanation

- `#!/bin/bash` batata hai ke script Bash shell mein run hogi.
- `dnf install -y httpd` supported Amazon Linux versions par Apache web server install karta hai.
- `systemctl enable --now httpd` Apache ko start karta hai aur automatic startup enable karta hai.
- `echo` website ki index file mein welcome message likhta hai.

### User Data Kaise Add Karte Hain?
1. EC2 service open karein.
2. Launch Instance par click karein.
3. AMI aur instance type select karein.
4. Advanced Details section open karein.
5. User Data field mein script paste karein.
6. Instance launch karein.
7. Instance ke start hone ke baad script ka result check karein.

Note: User Data scripts aam tor par first boot par run hoti hain. Dobara run karne ke liye additional configuration ki zaroorat ho sakti hai.

---

## 6. EC2 Lifecycle

### Definition
The EC2 lifecycle describes the different states an EC2 instance passes through during its operation.

### Lifecycle Kya Hai?
EC2 Lifecycle ka matlab hai instance ke create hone, start hone, run karne, stop hone aur terminate hone tak ke different stages.

### 6.1 Pending
Jab instance launch hota hai, to woh Pending state mein ja sakta hai. Is state mein AWS instance ko running ke liye prepare karta hai.

### 6.2 Running
Running state mein instance active hota hai aur computing tasks perform kar sakta hai.

### 6.3 Stopping
Stopping state mein instance ko band kiya ja raha hota hai.

### 6.4 Stopped
Stopped state mein instance band hota hai, lekin AWS account mein mojood rehta hai. Isay dobara start kiya ja sakta hai.

### 6.5 Shutting-down
Shutting-down state mein instance terminate hone ke process mein hota hai.

### 6.6 Terminated
Terminated state mein instance permanently remove ho chuka hota hai. Is instance ko dobara start nahi kiya ja sakta.

### Important Differences

- **Start:** Stopped instance ko dobara chalata hai.
- **Stop:** Instance ko temporary band karta hai.
- **Reboot:** Operating system ko restart karta hai.
- **Terminate:** Instance ko permanently remove karta hai.

### Lifecycle Mein Cost
Instance stop karne se compute charges aam tor par ruk jate hain, lekin attached EBS volumes aur kuch doosre resources ke charges jaari reh sakte hain.

Terminate karne se pehle storage aur data deletion settings check karni chahiye.

---

## 7. EC2 Pricing Models

### Definition
EC2 pricing models determine how users pay for computing capacity in AWS.

### Pricing Kya Hai?
AWS EC2 use karne ke liye different pricing models provide karta hai. In models ka maqsad users ko apni requirement aur budget ke mutabiq computing capacity use karne dena hai.

### 7.1 On-Demand Instances
On-Demand model mein long-term commitment ki zaroorat nahi hoti.

User instance ko apni requirement ke mutabiq use karta hai aur applicable usage charges pay karta hai.

**Best For:**
- Testing
- Short-term projects
- Unpredictable workloads

### 7.2 Reserved Instances
Reserved Instances aik ya teen saal ki commitment ke badlay eligible instance usage par discount provide kar sakte hain.

**Best For:**
Aise workloads jin ki computing requirements predictable hon.

### 7.3 Savings Plans
Savings Plans mein user aik ya teen saal ke liye eligible compute usage ki commitment karta hai.

Is commitment ke badlay eligible usage par lower prices mil sakti hain.

### 7.4 Spot Instances
Spot Instances AWS ki spare computing capacity use karte hain.

Ye On-Demand ke muqablay mein kaafi saste ho sakte hain, lekin AWS capacity ki zaroorat par inhein interrupt kar sakta hai.

**Best For:**
- Batch processing
- Flexible workloads
- Aise tasks jo interruption handle kar sakte hon

### Pricing Ko Control Karne Ke Tips
- Zaroorat ke mutabiq instance type select karein.
- Unused instances ko stop ya terminate karein.
- EBS volumes aur doosre resources check karein.
- AWS Budgets ke zariye spending alerts configure karein.
- Current cost estimate karne ke liye AWS Pricing Calculator use karein.

Important: Instance stop hone ke bawajood storage aur doosre resources ke charges aa sakte hain.

---

## 8. EC2 Scaling

### Definition
Scaling is the process of increasing or decreasing computing resources according to workload requirements.

### Scaling Kya Hai?
Scaling ka matlab hai demand ke mutabiq computing resources ko kam ya zyada karna.

Misal ke taur par, agar website par visitors bohat zyada ho jayein, to additional resources ki zaroorat ho sakti hai.

### 8.1 Vertical Scaling

Vertical Scaling mein aik hi EC2 instance ki capacity increase ya decrease ki jati hai.

Misal:
- Kam RAM wale instance se zyada RAM wale instance par move karna.
- Zyada CPU resources wala instance select karna.

Is process mein instance type change karne ke liye aksar instance ko stop karna parta hai.

### 8.2 Horizontal Scaling

Horizontal Scaling mein instances ki tadaad increase ya decrease ki jati hai.

Misal:
Agar website par traffic barh jaye, to hum aik server ke bajaye multiple EC2 instances use kar sakte hain.

### 8.3 Auto Scaling

Amazon EC2 Auto Scaling configured policies aur demand ke mutabiq instances ki tadaad automatically adjust kar sakti hai.

### Auto Scaling Ke Benefits
- Changing traffic ko handle karne mein madad karta hai.
- Application availability maintain karne mein madad karta hai.
- Zaroorat ke mutabiq computing capacity provide karta hai.
- Demand kam hone par extra capacity reduce kar sakta hai.

### 8.4 Load Balancer

Load Balancer incoming application traffic ko multiple targets, jaise EC2 instances, mein distribute karta hai.

Is se traffic aik hi server par concentrate hone ke bajaye multiple servers mein divide ho sakta hai.

### Real-Life Example
Agar online shopping website par normal din mein 100 users hon aur sale ke din 10,000 users aa jayein, to Auto Scaling additional instances add kar sakti hai aur Load Balancer traffic distribute kar sakta hai.

---

## 9. EC2, EBS Aur Auto Scaling Mein Farq

| Service | Kaam |
|---|---|
| EC2 | Cloud mein virtual server provide karta hai. |
| EBS | Persistent storage provide karta hai. |
| VPC | AWS mein virtual network provide karta hai. |
| Security Group | Network traffic control karta hai. |
| Key Pair | Secure authentication mein madad karta hai. |
| User Data | Initial setup automate karta hai. |
| Auto Scaling | Instances ki tadaad adjust karta hai. |
| Load Balancer | Traffic ko multiple targets mein distribute karta hai. |

---

## 10. Real-Life Example

Aik online shopping website banane ke liye hum AWS ki different services use kar sakte hain.

1. EC2 website ki application run karne ke liye virtual server provide karega.
2. EBS server ke operating system aur application ke liye storage provide karega.
3. VPC aur networking components server ki connectivity manage karenge.
4. Security Group required network traffic ko allow karega.
5. Key Pair Linux server par secure SSH access mein madad karega.
6. User Data web server ki installation automate kar sakta hai.
7. Lifecycle ki madad se instance ko start, stop aur terminate kar sakte hain.
8. Pricing model computing cost manage karne mein madad karega.
9. Auto Scaling demand ke mutabiq instances ki tadaad adjust kar sakti hai.
10. Load Balancer traffic ko multiple servers mein distribute kar sakta hai.

---

## 11. Amazon EC2 Ke Advantages

- Virtual servers jaldi launch kiye ja sakte hain.
- Different operating systems aur instance types available hain.
- Computing capacity ko workload ke mutabiq adjust kiya ja sakta hai.
- Different pricing models available hain.
- AWS ki doosri services ke saath integration hoti hai.
- Websites, applications aur testing environments ke liye useful hai.

## 12. Conclusion

Amazon EC2 AWS ki aik important computing service hai jo cloud mein virtual servers provide karti hai.

EBS storage provide karta hai, Networking server ko doosre resources ke saath communicate karne mein madad karti hai, Key Pair secure authentication ke liye use hota hai aur User Data initial setup automate karta hai.

EC2 Lifecycle instance ki different states ko explain karta hai. Pricing Models computing cost manage karne mein madad karte hain, jabke Scaling application ki changing demand ko handle karne mein help karti hai.

Ye tamam concepts AWS Cloud Computing aur Cloud Security seekhne ke liye bohat important hain.
