
# Class 12 – AWS VPC aur Networking

## 1. Introduction to AWS VPC

### Definition
Amazon VPC (Virtual Private Cloud) is a logically isolated virtual network in AWS where we can launch and manage AWS resources securely.

### Roman Urdu Explanation
AWS VPC aik private virtual network hota hai jo AWS cloud ke andar create kiya jata hai. Is network mein hum apne servers, databases aur doosre AWS resources ko control kar sakte hain.

VPC ki madad se hum decide karte hain:
- Hamare servers ka IP address kya hoga.
- Resources kis network mein honge.
- Internet access available hoga ya nahi.
- Kaun sa traffic allow ya block hoga.
- Public aur private resources ko kis tarah separate rakhna hai.

### Example
Agar hum AWS mein aik website host karna chahte hain, to hum VPC ke andar:
- Public subnet mein web server rakh sakte hain.
- Private subnet mein database rakh sakte hain.
- Security groups se traffic control kar sakte hain.

Is tarah website internet se accessible ho sakti hai, jabke database directly internet se accessible nahi hota.

---

## 2. What is AWS Networking?

### Definition
AWS Networking is the process of connecting AWS resources and controlling how data travels between them and external networks.

### Roman Urdu Explanation
AWS Networking ka matlab hai AWS resources ke darmiyan communication establish karna aur data ke flow ko manage karna.

Is mein ye components shamil hain:
- VPC
- Subnets
- IP Addresses
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Network ACLs
- VPC Endpoints

Ye components mil kar AWS network ko organize aur secure banate hain.

---

## 3. What is a CIDR Block?

### Definition
CIDR (Classless Inter-Domain Routing) is a method used to define a range of IP addresses.

### Roman Urdu Explanation
CIDR block IP addresses ki aik range define karta hai. VPC create karte waqt hum CIDR block select karte hain.

Example:

`10.0.0.0/16`

Is CIDR block mein bohat se private IPv4 addresses available hote hain jinhein hum apne network resources ke liye use kar sakte hain.

### Common CIDR Examples

- `10.0.0.0/16` – Large IP address range.
- `10.0.1.0/24` – Chhoti IP address range.
- `192.168.1.0/24` – Private network range.
- `172.16.0.0/16` – Private network range.

### CIDR ka `/16` aur `/24` kya matlab hai?

CIDR mein slash ke baad number batata hai ke IP address ke kitne bits network portion ke liye use ho rahe hain.

- `/16` mein IPv4 ke 16 bits network portion ke liye hote hain.
- `/24` mein 24 bits network portion ke liye hote hain.

IPv4 mein total 32 bits hote hain.

### Important Point
Chhota prefix number, jaise `/16`, aam tor par zyada addresses deta hai. Bara prefix number, jaise `/24`, kam addresses deta hai.

AWS VPC ke liye IPv4 CIDR block select karte waqt valid range aur doosre networks ke saath overlap ka khayal rakhna zaroori hai.

---

## 4. What is a Subnet?

### Definition
A subnet is a range of IP addresses within a VPC.

### Roman Urdu Explanation
Subnet VPC ka aik chhota network segment hota hai. Hum VPC ko different subnets mein divide kar sakte hain taake resources ko organize aur isolate kiya ja sake.

Example:

VPC CIDR: `10.0.0.0/16`

Is VPC ke andar:
- Public Subnet: `10.0.1.0/24`
- Private Subnet: `10.0.2.0/24`
- Database Subnet: `10.0.3.0/24`

Har subnet ko aik Availability Zone ke saath associate kiya jata hai.

### Subnet ki Types

#### A. Public Subnet
A public subnet woh subnet hota hai jiske associated route table mein Internet Gateway ki taraf route configured ho.

Is mein internet-facing resources, jaise public web servers, rakhe ja sakte hain.

Important: Sirf public subnet mein hone se instance automatically internet-accessible nahi hota. Us ke paas suitable public IP, routing aur security rules bhi hone chahiye.

#### B. Private Subnet
Private subnet mein aam tor par woh resources rakhe jate hain jinhein direct inbound internet access nahi dena hota.

Example:
- Databases
- Internal application servers
- Private backend services

Private subnet ke resources zaroorat ke mutabiq NAT Gateway ya VPC Endpoint ke through selected outbound connectivity hasil kar sakte hain.

---

## 5. What is an Availability Zone?

### Definition
An Availability Zone (AZ) is an isolated location within an AWS Region that contains one or more data centers.

### Roman Urdu Explanation
Availability Zone AWS Region ka aik separate infrastructure location hota hai. Multiple Availability Zones use karne se application ki availability aur fault tolerance improve ki ja sakti hai.

Example:
- Availability Zone A
- Availability Zone B
- Availability Zone C

Agar hum apni application ko multiple AZs mein deploy karte hain, to aik AZ mein problem hone ki surat mein doosri AZ application ko available rakhne mein madad kar sakti hai.

### Best Practice
Production applications ke liye zaroorat ke mutabiq multiple Availability Zones use karein.

---

## 6. What is an Internet Gateway?

### Definition
An Internet Gateway (IGW) is a VPC component that enables communication between a VPC and the internet when routing and security requirements are satisfied.

### Roman Urdu Explanation
Internet Gateway VPC ko internet ke saath communicate karne ka rasta provide karta hai.

Agar public subnet ke EC2 instance ko internet se communicate karwana ho, to aam tor par:
1. VPC ke saath Internet Gateway attach karein.
2. Subnet ki route table mein internet route add karein.
3. Internet route ko `0.0.0.0/0` se Internet Gateway ki taraf point karein.
4. Instance ko zaroorat ke mutabiq public IPv4 address dein.
5. Security Group aur Network ACL rules check karein.

### Example Route

`0.0.0.0/0 -> Internet Gateway`

Yahan `0.0.0.0/0` ka matlab tamam IPv4 destinations hain.

### Important Point
Internet Gateway attach karna akela kaafi nahi. Routing, IP addressing aur security rules bhi sahi hone chahiye.

---

## 7. What is a Route Table?

### Definition
A route table contains rules that determine where network traffic is directed.

### Roman Urdu Explanation
Route table network traffic ko sahi destination tak bhejne ke liye routes store karti hai.

Example:

| Destination | Target |
|---|---|
| `10.0.0.0/16` | Local |
| `0.0.0.0/0` | Internet Gateway |

`10.0.0.0/16` local route VPC ke andar communication ke liye hota hai.

`0.0.0.0/0` route IPv4 traffic ko default destination ki taraf bhejta hai. Agar target Internet Gateway ho, to subnet public routing ke liye configure hota hai.

### Route Table ki Types

- Public Route Table: Is mein Internet Gateway ki taraf default route ho sakta hai.
- Private Route Table: Is mein aam tor par direct Internet Gateway route nahi hota.
- Custom Route Table: Specific networking requirements ke liye banayi jati hai.

### Important Point
Har subnet aik route table se associated hota hai. Agar explicitly associate na kiya jaye, to subnet VPC ki main route table use karta hai.

---

## 8. What is a NAT Gateway?

### Definition
A NAT Gateway allows resources in a private subnet to initiate connections to external networks without allowing unsolicited inbound internet connections to those resources.

### Roman Urdu Explanation
NAT Gateway private subnet ke resources ko outbound internet connectivity provide kar sakta hai.

Example:
Aik private EC2 instance ko software updates download karni hain, lekin hum nahi chahte ke internet se koi bhi directly us instance ko access kare.

Is situation mein NAT Gateway use kiya ja sakta hai.

### NAT Gateway ka Basic Flow

Private EC2 Instance
-> Private Route Table
-> NAT Gateway
-> Internet Gateway
-> Internet

### Important Points
- Public NAT Gateway aam tor par public subnet mein create hota hai.
- Is ke saath Elastic IP associate hota hai.
- Public NAT Gateway ko internet tak traffic bhejne ke liye Internet Gateway route chahiye.
- Private subnet ki route table mein default route NAT Gateway ki taraf hota hai.
- NAT Gateway khud internet se shuru hone wali unsolicited inbound connections allow nahi karta.
- NAT Gateway par charges apply hote hain.

### NAT Gateway vs Internet Gateway

| Internet Gateway | NAT Gateway |
|---|---|
| VPC ko internet se connect karne mein madad karta hai. | Private resources ke outbound connections ke liye use hota hai. |
| Public subnet ki routing mein use hota hai. | Aam tor par private subnet ki default route ka target hota hai. |
| Public IP aur security configuration ke saath resources internet se reachable ho sakte hain. | Private instances ko direct inbound internet access dene ke liye nahi hota. |

---

## 9. What is a Security Group?

### Definition
A Security Group is a stateful virtual firewall that controls inbound and outbound traffic for supported AWS resources, such as EC2 instances.

### Roman Urdu Explanation
Security Group aik virtual firewall hai jo decide karta hai ke resource par kaun sa traffic allow hoga.

Hum inbound aur outbound rules define kar sakte hain.

### Inbound Rules
Inbound rules decide karte hain ke resource ke andar kaun sa traffic aa sakta hai.

Example:
- SSH: TCP port 22
- HTTP: TCP port 80
- HTTPS: TCP port 443

### Outbound Rules
Outbound rules decide karte hain ke resource se bahar kaun sa traffic ja sakta hai.

### Example
Agar hum web server ko HTTPS par accessible banana chahte hain, to Security Group mein TCP port 443 ke liye suitable inbound rule add kar sakte hain.

### Important Security Tips
- SSH port 22 ko `0.0.0.0/0` se open karne se avoid karein.
- SSH access ko apne trusted IP address tak restrict karein.
- Sirf required ports allow karein.
- Database ports ko public internet ke liye open na karein.
- Application ki requirements ke mutabiq outbound rules bhi restrict karein.

### Stateful ka Matlab
Security Group stateful hota hai. Agar allowed inbound connection establish hota hai, to us connection ka response traffic automatically allow hota hai, chahe us response ke liye alag outbound rule ki zaroorat na ho.

---

## 10. What is a Network ACL (NACL)?

### Definition
A Network Access Control List (NACL) is a subnet-level firewall that controls inbound and outbound traffic using allow and deny rules.

### Roman Urdu Explanation
Network ACL subnet ke level par traffic ko control karti hai.

Is mein:
- Inbound rules hotay hain.
- Outbound rules hotay hain.
- Allow rules hotay hain.
- Deny rules hotay hain.
- Rules ko number assign hota hai.

AWS rules ko lowest rule number se evaluate karta hai. Pehla matching rule apply hota hai. Agar koi rule match na kare, to traffic default behavior ke mutabiq deny hota hai.

### Security Group vs Network ACL

| Security Group | Network ACL |
|---|---|
| Resource level par traffic control karta hai. | Subnet level par traffic control karti hai. |
| Stateful hota hai. | Stateless hoti hai. |
| Allow rules support karta hai. | Allow aur deny dono rules support karti hai. |
| Rule order ko numbered priority ki tarah evaluate nahi karta. | Rules number ke order mein evaluate hotay hain. |

### Example
Agar aap kisi subnet mein specific IP range ka traffic block karna chahte hain, to NACL ka deny rule use kar sakte hain.

---

## 11. What is a VPC Endpoint?

### Definition
A VPC Endpoint enables private connectivity between a VPC and supported AWS services without requiring an Internet Gateway, NAT Gateway, or public IP for that service connection.

### Roman Urdu Explanation
VPC Endpoint ki madad se VPC ke resources kuch AWS services ko private network ke through access kar sakte hain.

Example:
Aik private EC2 instance ko Amazon S3 bucket access karni hai. Is ke liye S3 Gateway Endpoint use kiya ja sakta hai, jisse S3 traffic ke liye NAT Gateway ki zaroorat kam ya khatam ho sakti hai.

### VPC Endpoint ki Common Types

#### A. Gateway Endpoint
Gateway Endpoint Amazon S3 aur Amazon DynamoDB ke liye use hota hai.

#### B. Interface Endpoint
Interface Endpoint AWS PrivateLink use karta hai aur supported services ke liye VPC mein private network interfaces create karta hai.

### Benefits
- Private connectivity
- Public internet par dependence kam karna
- Network architecture ko secure banana
- Kuch situations mein NAT Gateway data-processing costs kam karna

### Important Point
Endpoint policies aur service resource policies ko sahi configure karna zaroori hai. Sirf endpoint create karne se har resource ko automatic permission nahi milti.

---

## 12. What is VPC Peering?

### Definition
VPC Peering is a networking connection between two VPCs that enables them to communicate using private IP addresses.

### Roman Urdu Explanation
Agar do VPCs ke resources ko private network ke through communicate karwana ho, to VPC Peering use ki ja sakti hai.

Example:
- VPC A mein application server hai.
- VPC B mein internal service hai.
- Dono VPCs ko private IP addresses ke through communicate karwana hai.

VPC Peering connection establish karne ke baad dono taraf suitable routes aur security rules configure karne hote hain.

### Important Points
- Dono VPCs ke CIDR blocks overlap nahi karne chahiye.
- Peering connection ko accept karna zaroori ho sakta hai.
- Dono VPCs ki route tables update karni hoti hain.
- Security Groups aur NACL rules communication ko allow karne chahiye.
- VPC Peering transitive routing support nahi karti.

### Transitive Routing ka Matlab
Agar VPC A, VPC B se peered hai aur VPC B, VPC C se peered hai, to VPC A automatically VPC C tak VPC B ke through communicate nahi kar sakti.

---

## 13. What is AWS Transit Gateway?

### Definition
AWS Transit Gateway is a networking service that connects multiple VPCs and on-premises networks through a central hub.

### Roman Urdu Explanation
Agar organization ke paas bohat sari VPCs hon, to har VPC ko individually doosri VPCs ke saath peer karna complicated ho sakta hai.

Transit Gateway aik central hub ki tarah kaam karta hai. Multiple VPCs aur supported external networks is hub ke saath connect ho sakte hain.

### Benefits
- Multiple VPCs ko connect karna.
- Network management ko simplify karna.
- Centralized routing.
- Large AWS network architectures ko organize karna.

### VPC Peering vs Transit Gateway

| VPC Peering | Transit Gateway |
|---|---|
| Aam tor par do VPCs ke darmiyan direct connection. | Multiple networks ke liye central hub. |
| Transitive routing support nahi karti. | Route configuration ke mutabiq networks ke darmiyan transit routing support kar sakta hai. |
| Chhoti architectures ke liye useful. | Bari network architectures ke liye useful. |

---

## 14. What is AWS VPN?

### Definition
AWS VPN provides encrypted connectivity between networks, such as an on-premises network and an AWS VPC.

### Roman Urdu Explanation
VPN ka matlab Virtual Private Network hai. Is ki madad se organization apne office network ko AWS ke saath encrypted connection ke zariye connect kar sakti hai.

AWS Site-to-Site VPN aam tor par on-premises network aur AWS ke darmiyan IPsec VPN tunnels use karti hai.

### Example
Aik company ka office Pakistan mein hai aur us ka application AWS mein host hai. Company apne office network se AWS VPC ko VPN ke zariye securely connect kar sakti hai.

### Benefits
- Encrypted communication.
- Office aur AWS network ke darmiyan connectivity.
- Private network resources tak controlled access.

### Important Point
VPN aur Direct Connect same cheez nahi hain. VPN encrypted tunnels use karti hai, jabke AWS Direct Connect AWS tak dedicated network connectivity provide karta hai. Dono ka design aur cost model different hota hai.

---

## 15. What is an Elastic IP Address?

### Definition
An Elastic IP address is a static public IPv4 address designed for dynamic cloud computing in AWS.

### Roman Urdu Explanation
Elastic IP aik static public IPv4 address hota hai jo AWS account ke saath allocate kiya jata hai aur supported resources ke saath associate kiya ja sakta hai.

Example:
Agar kisi internet-facing server ko stable public IPv4 address ki zaroorat ho, to Elastic IP use ki ja sakti hai.

### Important Points
- Elastic IP public IPv4 address hota hai.
- Is ko supported resource ke saath associate kiya ja sakta hai.
- Unused ya kuch specific configurations mein Elastic IP charges apply ho sakte hain.
- Har application ko Elastic IP ki zaroorat nahi hoti.

---

## 16. What is DNS in AWS?

### Definition
DNS (Domain Name System) translates domain names into IP addresses and supports other DNS records.

### Roman Urdu Explanation
DNS domain name ko IP address se resolve karne mein madad karta hai.

Example:
User browser mein `example.com` enter karta hai. DNS system us domain ke liye relevant IP address ya doosra DNS response provide karta hai.

### Amazon Route 53
Amazon Route 53 AWS ki scalable DNS service hai. Is se hum:
- DNS records manage kar sakte hain.
- Domain names ko resources ki taraf point kar sakte hain.
- Health checks aur supported routing policies configure kar sakte hain.
- Domain registration ki supported services use kar sakte hain.

### Important Point
DNS resolution aur network security alag concepts hain. DNS record create karne se Security Group ya routing automatically configure nahi hoti.

---

## 17. AWS VPC ka Complete Architecture Example

Hum aik secure web application architecture banate hain.

### Network Design

VPC CIDR: `10.0.0.0/16`

Public Subnet A: `10.0.1.0/24`

Public Subnet B: `10.0.2.0/24`

Private Subnet A: `10.0.11.0/24`

Private Subnet B: `10.0.12.0/24`

### Architecture Components
1. VPC – Main virtual network.
2. Public Subnets – Internet-facing load balancer ke liye.
3. Private Subnets – Application servers ke liye.
4. Internet Gateway – Public internet connectivity ke liye.
5. NAT Gateway – Zaroorat ke mutabiq private servers ki outbound IPv4 connectivity ke liye.
6. Route Tables – Traffic ko sahi destination tak bhejne ke liye.
7. Security Groups – Resource-level traffic control ke liye.
8. Network ACLs – Subnet-level traffic control ke liye.
9. VPC Endpoints – Supported AWS services ko private access dene ke liye.

### Traffic Flow
Internet User
-> Internet Gateway
-> Public Load Balancer
-> Private Application Server
-> Private Database

### Security Explanation
- Internet users sirf required public entry point tak access karte hain.
- Application servers private subnets mein rakhe jate hain.
- Database ko sirf required application servers se access diya jata hai.
- Database ka inbound access public internet ke liye open nahi hota.
- Security Groups mein sirf required ports allow kiye jate hain.

Production environment mein load balancer, application servers aur database ki high availability ke liye multiple Availability Zones aur suitable managed services use ki ja sakti hain.

---

## 18. AWS VPC Create Karne ka Practical Lab

### Lab Objective
AWS Console mein VPC aur subnet create karna aur basic network configuration samajhna.

### Step 1: AWS Console Login
1. AWS Management Console open karein.
2. Apne authorized AWS account se login karein.
3. Search bar mein `VPC` type karein.
4. Amazon VPC service open karein.

### Step 2: Create VPC
1. VPC Dashboard open karein.
2. `Create VPC` par click karein.
3. VPC ka naam enter karein, jaise `Student-VPC`.
4. IPv4 CIDR block enter karein: `10.0.0.0/16`.
5. Available options ko review karein.
6. `Create VPC` par click karein.

### Step 3: Create Public Subnet
1. Subnets section open karein.
2. `Create subnet` par click karein.
3. Apna VPC select karein.
4. Subnet ka naam `Public-Subnet` rakhein.
5. Availability Zone select karein.
6. IPv4 CIDR enter karein: `10.0.1.0/24`.
7. Subnet create karein.

### Step 4: Create Private Subnet
1. Dobara `Create subnet` par click karein.
2. Wohi VPC select karein.
3. Subnet ka naam `Private-Subnet` rakhein.
4. Zaroorat ke mutabiq Availability Zone select karein.
5. IPv4 CIDR enter karein: `10.0.2.0/24`.
6. Subnet create karein.

### Step 5: Internet Gateway Configure Karein
1. Internet Gateways section open karein.
2. `Create internet gateway` par click karein.
3. Naam `Student-IGW` rakhein.
4. Internet Gateway create karein.
5. `Attach to a VPC` option se apna VPC select karein.

### Step 6: Public Route Table Configure Karein
1. Route Tables section open karein.
2. Apne VPC ke liye route table create karein ya suitable existing route table select karein.
3. Public route table ki Routes tab open karein.
4. `Edit routes` select karein.
5. Destination `0.0.0.0/0` add karein.
6. Target mein Internet Gateway select karein.
7. Changes save karein.
8. Subnet associations mein Public-Subnet associate karein.

### Step 7: Public IPv4 Auto-Assignment
Agar public subnet mein test EC2 instance ko automatic public IPv4 address dena ho:
1. Subnets section open karein.
2. Public subnet select karein.
3. Subnet actions mein edit IP address assignment settings open karein.
4. Auto-assign public IPv4 setting enable karein, agar zaroorat ho.

Note: Yeh setting aam tor par naye instances par apply hoti hai. Existing instance ko public IPv4 dene ke liye instance ki IP configuration ya Elastic IP ki zaroorat ho sakti hai.

### Step 8: Verify Configuration
Check karein:
- VPC create ho chuka hai.
- Dono subnets correct VPC ke andar hain.
- Internet Gateway VPC ke saath attached hai.
- Public route table mein correct route hai.
- Public subnet route table ke saath associated hai.

### Lab Safety
- Test resources ko production resources se separate rakhein.
- EC2 instance launch karne se pehle security rules review karein.
- SSH ko `0.0.0.0/0` se open na karein.
- NAT Gateway aur doosre paid resources create karne se pehle cost samajh lein.
- Lab complete hone ke baad unnecessary resources delete kar dein.

---

## 19. AWS VPC Security Best Practices

1. Public aur private subnets ko zaroorat ke mutabiq separate rakhein.
2. Database ko direct public internet access na dein.
3. Security Groups mein least privilege follow karein.
4. SSH aur RDP access ko trusted IP ranges tak restrict karein.
5. Sirf required inbound aur outbound traffic allow karein.
6. Sensitive AWS services ke liye VPC Endpoints consider karein.
7. Production resources ko multiple Availability Zones mein deploy karein.
8. VPC Flow Logs enable karne par consider karein, taake network traffic metadata analyze ki ja sake.
9. Route tables aur NACL rules regularly review karein.
10. Unused public IPs aur networking resources ko review karein.
11. AWS IAM permissions ko least privilege ke mutabiq configure karein.
12. CloudTrail aur suitable monitoring tools use karein.
13. Network architecture ko document karein.
14. Costs aur resource usage regularly monitor karein.

---

## 20. Common AWS VPC Mistakes

### Mistake 1: Internet Gateway Attach Hai Lekin Internet Access Nahi
Possible reasons:
- Route table mein default route missing hai.
- Subnet wrong route table use kar raha hai.
- Instance ke paas public IPv4 address nahi hai.
- Security Group traffic block kar raha hai.
- Network ACL rules traffic block kar rahe hain.

### Mistake 2: Private Instance Internet Access Nahi Kar Raha
Possible reasons:
- NAT Gateway configured nahi hai.
- Private route table mein correct NAT route missing hai.
- NAT Gateway ke public subnet ki routing incorrect hai.
- Security rules ya DNS configuration mein problem hai.

### Mistake 3: VPC Peering Ke Baad Communication Nahi Ho Rahi
Possible reasons:
- Peering connection active nahi hai.
- Route tables update nahi ki gayin.
- Security Group ya NACL traffic block kar raha hai.
- CIDR blocks overlap karte hain.

### Mistake 4: Database Publicly Accessible Hai
Possible reasons:
- Database ko public access ke liye configure kiya gaya hai.
- Security Group mein overly broad inbound rule hai.
- Network architecture mein unnecessary exposure hai.

Solution:
Database ko private networking mein rakhein aur inbound access sirf authorized application resources tak restrict karein.

---

## 21. Important AWS Networking Ports

| Service | Port | Protocol |
|---|---|---|
| SSH | 22 | TCP |
| HTTP | 80 | TCP |
| HTTPS | 443 | TCP |
| RDP | 3389 | TCP |
| DNS | 53 | UDP/TCP |
| MySQL | 3306 | TCP |
| PostgreSQL | 5432 | TCP |

Important: Kisi port ko open karne se pehle verify karein ke application ko waqai us port ki zaroorat hai.

---

## 22. Interview Questions and Answers

### Q1: What is Amazon VPC?
Answer: Amazon VPC is a logically isolated virtual network in AWS where we can launch and manage resources.

### Q2: What is a subnet?
Answer: A subnet is a range of IP addresses within a VPC.

### Q3: What is the difference between a public and private subnet?
Answer: A public subnet has a route to an Internet Gateway. A private subnet does not have a direct route to an Internet Gateway for general internet access.

### Q4: What is an Internet Gateway?
Answer: An Internet Gateway enables internet communication for appropriately configured VPC resources.

### Q5: What is a NAT Gateway?
Answer: A NAT Gateway allows private subnet resources to initiate outbound connections to external networks without allowing unsolicited inbound internet connections.

### Q6: What is a route table?
Answer: A route table contains rules that direct network traffic to destinations.

### Q7: What is a Security Group?
Answer: A Security Group is a stateful virtual firewall for supported AWS resources.

### Q8: What is a Network ACL?
Answer: A Network ACL is a stateless subnet-level firewall that supports allow and deny rules.

### Q9: What is a VPC Endpoint?
Answer: A VPC Endpoint provides private connectivity to supported AWS services.

### Q10: What is VPC Peering?
Answer: VPC Peering connects two VPCs so they can communicate using private IP addresses.

### Q11: What is AWS Transit Gateway?
Answer: AWS Transit Gateway connects multiple VPCs and other supported networks through a central hub.

### Q12: Why do we use multiple Availability Zones?
Answer: Multiple Availability Zones can improve application availability and fault tolerance.

### Q13: What is CIDR?
Answer: CIDR is a method for defining IP address ranges.

### Q14: What is an Elastic IP?
Answer: An Elastic IP is a static public IPv4 address that can be associated with supported AWS resources.

### Q15: What is VPC Flow Logs?
Answer: VPC Flow Logs capture information about IP traffic to and from network interfaces in a VPC, subnet, or supported resource.

---

## 23. Class Summary

Is class mein hum ne seekha:

- AWS VPC kya hai.
- AWS Networking ka basic concept.
- CIDR blocks aur IP address ranges.
- Public aur private subnets.
- Availability Zones.
- Internet Gateway aur NAT Gateway.
- Route Tables.
- Security Groups aur Network ACLs.
- VPC Endpoints.
- VPC Peering aur Transit Gateway.
- AWS VPN aur Elastic IP.
- Amazon Route 53 aur DNS.
- Basic VPC creation lab.
- AWS networking security best practices.

### Final Concept
AWS VPC AWS cloud ka aik important networking component hai. Is ki madad se hum apne cloud resources ko logically organize karte hain, traffic control karte hain aur secure network architecture design karte hain.

Secure AWS architecture ke liye correct routing, least-privilege security rules, private subnets aur regular monitoring bohat important hain.
