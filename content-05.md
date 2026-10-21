# Class 5 - Amazon EC2 Basics

## 1. Amazon EC2 Kya Hai?

**Definition:**

Amazon EC2 ka full form Amazon Elastic Compute Cloud hai. Ye AWS ki aik cloud service hai jo users ko virtual servers provide karti hai.

**Explanation:**

Amazon EC2 aik aisi service hai jis ki madad se hum internet ke zariye cloud mein apna virtual computer ya server bana sakte hain. Is server par hum websites, applications aur software chala sakte hain. Humein apna physical server khareedne ki zaroorat nahi hoti.

**Example:**

Agar hum apni website internet par chalana chahte hain, to hum Amazon EC2 par virtual server launch kar sakte hain.

## 2. EC2 Instance Kya Hai?

**Definition:**

EC2 instance aik virtual server hota hai jo AWS cloud mein run karta hai.

**Explanation:**

Jab hum AWS mein EC2 server launch karte hain, to usay EC2 instance kehte hain. Is mein CPU, RAM, storage aur operating system hota hai. Hum is par apni applications aur websites chala sakte hain.

**Example:**

Hum Ubuntu Linux ke sath EC2 instance launch kar ke Linux commands practice kar sakte hain.

## 3. Amazon EC2 Ki Features

### 3.1 Scalability

Scalability ka matlab hai zaroorat ke mutabiq server ke resources ko barhana ya kam karna.

**Example:**

Agar website par visitors zyada ho jayein, to hum apne server ki capacity barha sakte hain.

### 3.2 Flexibility

Flexibility ka matlab hai apni zaroorat ke mutabiq operating system, server type aur storage select karna.

**Example:**

Hum apni requirement ke mutabiq Linux ya Windows server select kar sakte hain.

### 3.3 Pay-As-You-Go

Is ka matlab hai ke hum selected pricing model ke mutabiq use kiye gaye resources ke charges pay karte hain.

**Example:**

EC2 use karte waqt instance, storage aur data transfer ke charges lag sakte hain. Is liye AWS billing check karna zaroori hai.

## 4. AMI Kya Hai?

AMI ka full form Amazon Machine Image hai.

AMI aik template hota hai jis ki madad se hum EC2 instance launch karte hain. Is mein operating system aur software ki configuration shamil ho sakti hai.

**Example:**

Agar hum Ubuntu Server ka AMI select karte hain, to hamara EC2 instance Ubuntu operating system ke sath launch hoga.

## 5. Key Pair Kya Hai?

Key pair mein public key aur private key hoti hain. Ye EC2 instance ko securely access karne ke liye use hota hai.

Private key ko hamesha safe rakhna chahiye aur kisi ke sath share nahi karna chahiye.

**Example:**

Linux EC2 instance ko SSH ke zariye access karne ke liye private key use ki ja sakti hai.

## 6. Security Group Kya Hai?

Security group aik virtual firewall hota hai jo EC2 instance ke network traffic ko control karta hai.

Ye decide karta hai ke kaunsa traffic server mein aa sakta hai aur kaunsa bahar ja sakta hai.

**Important Ports:**

- Port 22 SSH ke liye use hota hai.
- Port 80 HTTP ke liye use hota hai.
- Port 443 HTTPS ke liye use hota hai.

**Example:**

Agar hum Linux server ko SSH se access karna chahte hain, to security group mein port 22 ka rule configure karte hain.

**Security Tip:**

Sirf zaroori ports allow karein aur SSH access ko apne trusted IP address tak limited rakhein.

## 7. EC2 Storage Kya Hai?

Storage ka matlab hai server mein data, files aur applications ko save karne ki jagah.

### 7.1 Amazon EBS

EBS ka full form Elastic Block Store hai.

EBS aik storage service hai jo EC2 instance ke sath attach ki ja sakti hai. Is mein operating system, applications aur important data store kiya ja sakta hai.

**Example:**

Hum EBS volume mein apni website ki files aur doosra data store kar sakte hain.

### 7.2 Instance Store

Instance store kuch EC2 instances mein available temporary storage hoti hai.

Is storage ka data instance ya host ki lifecycle se related events par lose ho sakta hai. Is liye important data ke liye backup aur suitable persistent storage use karni chahiye.

## 8. EC2 Instance States

EC2 instance ki mukhtalif states hoti hain.

- **Pending:** Instance start ho raha hota hai.
- **Running:** Instance chal raha hota hai.
- **Stopping:** Instance band ho raha hota hai.
- **Stopped:** Instance band hota hai aur dobara start kiya ja sakta hai.
- **Shutting-down:** Instance terminate hone ki process mein hota hai.
- **Terminated:** Instance permanently terminate ho chuka hota hai.

**Important Note:**

Stopped aur terminated mein farq hota hai. Stopped instance ko dobara start kiya ja sakta hai, lekin terminated instance ko dobara start nahi kiya ja sakta.

## 9. EC2 Instance Launch Karne Ka Tarika

Amazon EC2 instance launch karne ke liye ye steps follow karein:

1. AWS Management Console mein login karein.
2. EC2 service open karein.
3. Launch Instance par click karein.
4. Apne instance ka name likhein.
5. AMI select karein.
6. Instance type select karein.
7. Key pair create ya select karein.
8. Security group configure karein.
9. Storage settings select karein.
10. Launch Instance par click karein.
11. Instances page par ja kar instance ka status check karein.

**Explanation:**

In steps ki madad se hum AWS cloud mein apna virtual server bana sakte hain. Instance launch karne se pehle security settings aur pricing zaroor check karein.

## 10. EC2 Instance Types

EC2 mein mukhtalif types ke servers available hote hain.

- **General Purpose:** Normal applications aur websites ke liye.
- **Compute Optimized:** CPU-intensive tasks ke liye.
- **Memory Optimized:** Zyada memory ki zaroorat wali applications ke liye.
- **Storage Optimized:** Zyada ya fast storage ki zaroorat wale tasks ke liye.
- **Accelerated Computing:** GPU aur machine learning jaise workloads ke liye.

Har instance type ki performance aur cost mukhtalif ho sakti hai.

## 11. Amazon EC2 Ke Uses

Amazon EC2 ko mukhtalif kaamon ke liye use kiya jata hai.

- Websites host karne ke liye.
- Web applications run karne ke liye.
- Software testing aur development ke liye.
- Database servers chalane ke liye.
- Linux aur Windows servers use karne ke liye.
- Cloud computing practice karne ke liye.
- Data processing ke liye.

## 12. Amazon EC2 Ke Advantages

- Hum apni zaroorat ke mutabiq server select kar sakte hain.
- Computing resources ko adjust kar sakte hain.
- Websites aur applications cloud mein chala sakte hain.
- Mukhtalif operating systems use kar sakte hain.
- AWS ki doosri services ke sath integrate kar sakte hain.
- Physical server khareedne aur maintain karne ki zaroorat kam ho sakti hai.

## 13. Amazon EC2 Ke Disadvantages

- AWS use karne ke liye technical knowledge ki zaroorat hoti hai.
- Ghalat security settings se server ko risk ho sakta hai.
- Resources active rehne par unexpected charges aa sakte hain.
- Data ki safety ke liye backup aur monitoring zaroori hoti hai.
- Beginners ke liye configuration samajhna mushkil ho sakta hai.

## 14. EC2 Security Best Practices

- Private key ko secure rakhein.
- Security group mein sirf required ports allow karein.
- IAM users ko sirf zaroori permissions dein.
- Operating system aur software ko update rakhein.
- Important data ka backup rakhein.
- AWS billing aur usage regularly check karein.
- Jo test instances use nahi ho rahe, unhein stop ya terminate karein.
- Server ki monitoring aur security ka khayal rakhein.

## 15. Real-Life Example

Suppose hum aik online shopping website banana chahte hain.

Sab se pehle hum AWS par EC2 instance launch karenge. Phir Ubuntu Server ka AMI select karenge aur server par web server install karenge. Us ke baad security group mein required HTTP aur HTTPS traffic allow karenge. Website ki files upload kar ke domain aur networking configure karenge.

Is tarah hum Amazon EC2 ki madad se apni website internet par host kar sakte hain.

## 16. Important Terms

- **AWS:** Amazon Web Services.
- **EC2:** Elastic Compute Cloud.
- **Instance:** Cloud mein virtual server.
- **AMI:** EC2 instance launch karne ka template.
- **EBS:** EC2 ke liye block storage service.
- **Security Group:** Virtual firewall.
- **Key Pair:** Public key aur private key ka combination.
- **Scalability:** Resources ko zaroorat ke mutabiq adjust karna.
- **SSH:** Secure Shell, jo remote server access karne ke liye use hota hai.
- **Region:** AWS infrastructure ka geographical area.
- **Availability Zone:** AWS Region ke andar alag infrastructure location.

## 17. Conclusion

Amazon EC2 AWS ki aik important cloud service hai jo humein virtual servers provide karti hai. Is ki madad se hum websites host kar sakte hain, applications run kar sakte hain aur different operating systems use kar sakte hain.

EC2 use karte waqt humein security, storage, instance configuration aur billing ka khaas khayal rakhna chahiye.

**Short Summary:**

Amazon EC2 aik AWS service hai jo cloud mein virtual server provide karti hai. Is server par hum websites, applications aur software chala sakte hain.
