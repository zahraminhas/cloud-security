# Class 4 - Cloud Security

## 1. Root User

### Definition
Root User AWS account ki original identity hoti hai.

### Tafseel
Root User account ka main owner hota hai. Is ke paas AWS account ki important settings aur services ka access hota hai. Is liye isay ehtiyat se use karna chahiye.

### Best Practices
- Root User par MFA enable karein.
- Strong password rakhein.
- Credentials kisi ke saath share na karein.
- Daily tasks ke liye IAM User use karein.

## 2. Least Privilege

### Definition
Least Privilege ka matlab user ko sirf zaroori permissions dena hai.

### Tafseel
Har user ko sirf apne kaam ke mutabiq access milna chahiye.

### Example
Agar employee ko sirf S3 files dekhni hain, to usay sirf read permissions dein.

### Benefits
- Unauthorized access kam hota hai.
- Data secure rehta hai.
- Security improve hoti hai.

## 3. MFA (Multi-Factor Authentication)

### Definition
MFA login ke waqt identity verify karne ke liye do ya zyada mukhtalif verification factors use karta hai.

### Tafseel
Password ke ilawa authenticator app ka code ya security key use ki ja sakti hai.

### Benefits
- Account security strong hoti hai.
- Stolen password ke misuse ka risk kam hota hai.
- Unauthorized login se protection milti hai.

## 4. Encryption

### Definition
Encryption readable data ko cryptographic algorithm aur key ki madad se unreadable form mein convert karta hai.

### Tafseel
Encryption sensitive data ko protect karti hai. Authorized user sahi key aur permissions se data decrypt kar sakta hai.

### Types of Encryption

#### Encryption at Rest
Storage mein saved data ko encrypt karna.

Example: AWS S3 mein files encrypt karna.

#### Encryption in Transit
Network par transfer hone wale data ko encrypt karna.

Example: HTTPS ke zariye data transfer.

### Benefits
- Data confidentiality protect hoti hai.
- Sensitive information secure rehti hai.
- Unauthorized logon ke liye data parhna mushkil hota hai.

## 5. AWS KMS (Key Management Service)

### Definition
AWS KMS ek service hai jo cryptographic keys ko create, manage aur control karne mein madad karti hai.

### Tafseel
AWS KMS encryption keys ko manage karti hai jo data encrypt aur decrypt karne ke liye use hoti hain.

### Example
AWS S3 mein files ko AWS KMS key ke zariye encrypt karna.

### Benefits
- Keys ko manage karna asaan hota hai.
- Key access control kiya ja sakta hai.
- AWS services ke saath encryption use ki ja sakti hai.

## 6. Federation (Identity Federation)

### Definition
Federation user ko trusted Identity Provider ki identity ke zariye doosri service tak access deti hai.

### Tafseel
Company ka employee apni existing organization identity se AWS mein login kar sakta hai, agar federation configure ki gayi ho.

### Example
Employee apni company ke login system se AWS access hasil karta hai.

### How Federation Works
1. User company ke login system mein sign in karta hai.
2. Identity Provider user ki identity verify karta hai.
3. AWS configured federation ke zariye authentication accept karta hai.
4. AWS assigned role aur permissions ke mutabiq access deta hai.

### Benefits
- Centralized identity management hoti hai.
- Multiple passwords ki zaroorat kam hoti hai.
- Employee access manage karna asaan hota hai.

## 7. Difference Between Concepts

| Concept | Purpose |
|---|---|
| Root User | AWS account ki original identity |
| Least Privilege | Sirf required permissions dena |
| MFA | Additional login verification |
| Encryption | Data ko protect karna |
| AWS KMS | Encryption keys manage karna |
| Federation | Trusted identity se access lena |

## 8. Real-Life Example

Ek company AWS use karti hai.

- Root User: AWS account ka main owner.
- Least Privilege: Developer ko sirf required permissions milti hain.
- MFA: Employee additional verification se login karta hai.
- Encryption: Company ki files encrypted hoti hain.
- AWS KMS: Encryption keys manage hoti hain.
- Federation: Employee company identity se AWS mein login karta hai.

## 9. Conclusion

Root User, Least Privilege, MFA, Encryption, AWS KMS aur Federation cloud security ke important concepts hain.

In concepts ko sahi tarah use karne se AWS account ki security improve hoti hai, unnecessary access kam hota hai aur sensitive data protect rehta hai.

## 10. Quick Revision

1. Root User - AWS account ki original identity.
2. Least Privilege - Sirf zaroori permissions.
3. MFA - Additional verification.
4. Encryption - Data ko unreadable form mein convert karna.
5. AWS KMS - Encryption keys ka management.
6. Federation - Trusted identity se AWS access.

