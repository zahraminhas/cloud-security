# Class 3 – Migration, Shared Responsibility & IAM Basics

## 1. Cloud Migration

### Cloud Migration Kya Hai?

Cloud Migration ka matlab hai apne **data, applications, databases, servers aur IT resources ko local/on-premises system se cloud par move karna**.

**Example:**  
Agar kisi company ka website aur database uske physical server par hai aur company usay AWS par move kar deti hai, to is process ko Cloud Migration kehte hain.

### Cloud Migration Kyun Ki Jati Hai?

- Cost kam karne ke liye
- Resources ko easily increase/decrease karne ke liye
- Better availability ke liye
- Fast deployment ke liye
- Backup aur recovery ke liye
- Physical hardware ki zaroorat kam karne ke liye

---

## 2. Cloud Migration Strategies

### 2.1 Rehost – Lift and Shift

Rehost ka matlab hai application ko **minimum changes ke sath cloud par move karna**.

**Example:**  
Existing application ko local server se AWS EC2 par move karna.

### 2.2 Replatform

Replatform ka matlab hai application ko cloud par move karte waqt **kuch improvements** karna.

**Example:**  
Database ko cloud ki managed database service par move karna.

### 2.3 Refactor

Refactor ka matlab hai application ko **redesign ya rewrite karna** taa-ke woh cloud ki modern services ka full benefit le sake.

### 2.4 Repurchase

Repurchase ka matlab hai purani application ko replace karke **new cloud-based software/service use karna**.

### 2.5 Retain

Retain ka matlab hai application ko cloud par migrate na karna aur **existing environment mein rakhna**.

### 2.6 Retire

Retire ka matlab hai **old ya unused application ko remove kar dena**.

---

## 3. Benefits of Cloud Migration

### Cost Saving

Physical servers ko purchase aur maintain karne ka cost kam ho sakta hai.

### Scalability

Demand ke mutabiq cloud resources ko increase ya decrease kiya ja sakta hai.

### Availability

Cloud services high availability provide kar sakti hain.

### Flexibility

Users different locations se internet ke through cloud resources access kar sakte hain.

### Backup and Recovery

Cloud mein data ka backup aur recovery easy ho sakti hai.

### Fast Deployment

Cloud resources ko quickly deploy kiya ja sakta hai.

---

## 4. Shared Responsibility Model

### Shared Responsibility Model Kya Hai?

Shared Responsibility Model ka matlab hai ke **cloud security ki responsibility cloud provider aur customer ke darmiyan divide hoti hai**.

**AWS = Security OF the Cloud**

**Customer = Security IN the Cloud**

Yani AWS cloud ki infrastructure ko protect karta hai, jab ke customer apne data, accounts, applications aur configurations ko secure karta hai.

---

## 5. Cloud Provider Ki Responsibility

Cloud provider underlying cloud infrastructure ko secure karta hai.

Is mein include hain:

- Physical Data Centers
- Physical Servers
- Networking Infrastructure
- Hardware
- Physical Security
- Core Cloud Infrastructure

**Example:**  
AWS apne physical data centers aur servers ki security manage karta hai.

---

## 6. Customer Ki Responsibility

Customer apne cloud resources aur data ki security ka responsible hota hai.

Is mein include ho sakta hai:

- Data protection
- User accounts
- Passwords
- IAM permissions
- Application security
- Operating system configuration
- Network configuration
- Encryption
- Security groups
- Access control

---

## 7. Shared Responsibility Ka Simple Example

Isay ghar ki example se samjhein.

Ghar ka owner building aur main structure ki security ka responsible hai.

Lekin ghar mein rehne wala person:

- Apna room lock karta hai
- Apni important cheezen protect karta hai
- Keys ko safe rakhta hai

Isi tarah cloud mein:

**Cloud Provider:** Cloud infrastructure protect karta hai.

**Customer:** Apna data, account, application aur configuration protect karta hai.

---

## 8. Responsibility Service Ke Mutabiq

### IaaS – Infrastructure as a Service

IaaS mein customer ko zyada cheezen manage karni hoti hain:

- Operating System
- Applications
- Data
- Configuration

### PaaS – Platform as a Service

PaaS mein cloud provider underlying infrastructure aur platform ka zyada part manage karta hai.

Customer mainly application aur data par focus karta hai.

### SaaS – Software as a Service

SaaS mein provider application aur infrastructure ka major part manage karta hai.

Customer ko mainly account, access, data aur permissions secure karni hoti hain.

---

## 9. IAM – Identity and Access Management

### IAM Kya Hai?

IAM ka full form hai:

**Identity and Access Management**

IAM control karta hai ke:

**Kaun cloud resources ko access kar sakta hai aur woh kya actions perform kar sakta hai.**

Simple words:

**IAM = Users + Permissions + Access Control**

---

## 10. IAM Kyun Important Hai?

IAM:

- Unauthorized access ko prevent karta hai
- Users ko manage karta hai
- Permissions control karta hai
- Sensitive data protect karta hai
- Different users ko different access deta hai
- Security improve karta hai

---

## 11. IAM User

IAM User ek identity hoti hai jo kisi person ya application ko represent karti hai.

**Example:**  
Company Ali ke liye IAM User create karti hai aur usay required permissions deti hai.

---

## 12. IAM Group

IAM Group multiple IAM Users ka collection hota hai.

**Example:**

Company ek **Developers Group** banati hai aur tamam developers ko is group mein add kar deti hai.

---

## 13. IAM Policy

IAM Policy rules ka set hota hai jo define karta hai ke user ya role:

- Kya kar sakta hai
- Kis resource ko access kar sakta hai
- Kaunsa action allowed hai
- Kaunsa action denied hai

**Example:**  
User ko files read karne ki permission hai lekin delete karne ki permission nahi.

---

## 14. IAM Role

IAM Role permissions ka ek set hota hai jise users, applications ya AWS services zaroorat ke mutabiq assume kar sakti hain.

**Example:**  
EC2 instance ko IAM Role diya ja sakta hai taa-ke woh S3 bucket se files access kar sake.

---

## 15. Authentication

Authentication ka matlab hai **user ki identity verify karna**.

**Simple Question:**

> Who are you?

**Example:**  
Username aur password se login karna authentication hai.

---

## 16. Authorization

Authorization ka matlab hai check karna ke authenticated user ko **kya karne ki permission hai**.

**Simple Question:**

> What are you allowed to do?

**Example:**  
User ko file read karne ki permission hai lekin delete karne ki permission nahi.

---

## 17. Authentication vs Authorization

| Authentication | Authorization |
|---|---|
| Identity verify karta hai | Permissions check karta hai |
| Who are you? | What can you do? |
| Login example hai | Access permission example hai |

---

## 18. Principle of Least Privilege

Least Privilege ka matlab hai:

**User ya application ko sirf utni permissions dena jitni usay apna kaam perform karne ke liye zaroori hain.**

**Example:**  
Agar employee ko sirf files read karni hain to usay files delete karne ki permission nahi deni chahiye.

Is se security risk kam hota hai.

---

## 19. Multi-Factor Authentication – MFA

MFA ka full form hai:

**Multi-Factor Authentication**

MFA security ki extra layer provide karta hai.

**Example:**

1. Password
2. Authentication App ka Verification Code

Agar attacker ko password mil bhi jaye to second factor ke baghair account access karna mushkil ho sakta hai.

---

## 20. IAM Best Practices

### 1. Least Privilege Use Karein

Users ko sirf required permissions dein.

### 2. MFA Enable Karein

Important accounts, especially administrator accounts, par MFA use karein.

### 3. IAM Roles Use Karein

Jahan suitable ho applications aur AWS services ke liye roles use karein.

### 4. Credentials Protect Karein

Passwords aur access keys kisi ke sath share na karein.

### 5. Permissions Review Karein

Regularly check karein ke users ke paas unnecessary permissions to nahi.

### 6. Unused Accounts Remove Karein

Jo accounts use nahi ho rahe unhein disable/remove karein.

### 7. Strong Passwords Use Karein

Strong aur unique passwords use karein.

---

## 21. Migration + Shared Responsibility + IAM

Ye teen concepts cloud security mein connected hain.

### Migration

IT resources ko cloud mein move karta hai.

### Shared Responsibility

Batata hai ke cloud security ki responsibility kis ki hai.

### IAM

Batata hai ke cloud resources ko **kaun access kar sakta hai aur kya kar sakta hai**.

### Simple Flow

**Migration → Cloud Resources → Security Responsibilities → IAM Access Control**

---

## 22. Real-Life Example

Suppose ek university apna student management system local server se AWS par move karti hai.

### Step 1 – Migration

University application aur database ko AWS par move karti hai.

### Step 2 – Shared Responsibility

AWS physical cloud infrastructure ki security manage karta hai.

University apne:

- Student Data
- User Accounts
- Applications
- Permissions
- Configurations

ki security manage karti hai.

### Step 3 – IAM

University different users ko different permissions deti hai.

- **Administrator:** Required administrative access
- **Developer:** Application-related access
- **Database Team:** Database-related access
- **Student:** Sirf required application access

Is tarah unauthorized access ka risk kam hota hai.

---

## 23. Important Terms

**Cloud Migration:** IT resources ko cloud par move karna.

**Rehost:** Application ko minimum changes ke sath cloud par move karna.

**Replatform:** Application ko cloud par move karte waqt improvements karna.

**Refactor:** Application ko cloud-native features ke liye redesign karna.

**Repurchase:** Existing software ko replace karke cloud-based software use karna.

**Retain:** Application ko existing environment mein rakhna.

**Retire:** Unused application ko remove karna.

**Shared Responsibility Model:** Cloud security responsibilities ko provider aur customer ke darmiyan divide karta hai.

**IAM:** Identity and Access Management.

**User:** Kisi person ya application ki identity.

**Group:** Multiple IAM users ka collection.

**Policy:** Permissions aur allowed/denied actions define karti hai.

**Role:** Permissions ka set jo trusted entity assume kar sakti hai.

**Authentication:** Identity verify karna.

**Authorization:** Permissions check karna.

**Least Privilege:** Sirf required permissions dena.

**MFA:** Extra authentication/security factor.

---

## 24. Summary

Cloud Migration ka matlab IT resources ko cloud par move karna hai.

Migration ki important strategies:

- Rehost
- Replatform
- Refactor
- Repurchase
- Retain
- Retire

Shared Responsibility Model ke according cloud provider aur customer dono ki security responsibilities hoti hain.

IAM ka full form **Identity and Access Management** hai. IAM users, groups, policies, roles aur permissions ke through cloud resources ka access control karta hai.

### Key Point

> Migration resources ko cloud par move karta hai, Shared Responsibility security responsibilities define karta hai, aur IAM cloud resources ka access control karta hai.
