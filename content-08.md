
# Class 8 — Amazon S3 (Simple Storage Service)

## 1. What Is Amazon S3?

### Definition
Amazon Simple Storage Service (Amazon S3) is an object storage service provided by Amazon Web Services (AWS). It allows users to store, retrieve, and manage data from anywhere through the internet or supported network connections.

### Roman Urdu Explanation
Amazon S3 AWS ki aik cloud storage service hai. Iski madad se hum internet par apni files aur data store kar sakte hain.

Misal ke taur par, agar aapke paas pictures, videos, documents, backups ya website ki files hain, to aap inhein Amazon S3 mein store kar sakti hain.

S3 mein data objects ki form mein store hota hai. Is data ko manage karne ke liye buckets use hoti hain.

### Real-Life Example
Aap apne computer mein pictures save karti hain. Isi tarah Amazon S3 mein bhi pictures upload kar sakti hain, lekin files cloud mein store hoti hain.

Aap authorized access ke zariye in files ko retrieve kar sakti hain.

### Uses of Amazon S3

- Images aur videos store karna.
- Documents aur PDFs store karna.
- Data backups rakhna.
- Application files store karna.
- Website ke static content ko host karna.
- Logs aur data files store karna.
- Data analytics ke liye files rakhna.
- Disaster recovery ke liye backups store karna.

## 2. What Is Object Storage?

### Definition
Object storage is a data storage architecture in which data is stored as objects along with associated metadata and a unique identifier.

### Roman Urdu Explanation
Object storage mein data objects ki form mein save hota hai. Har object ke andar aam tor par teen cheezein hoti hain:

1. **Data:** Asal file, jaise image, video ya PDF.
2. **Metadata:** File ke bare mein information, jaise content type aur creation details.
3. **Unique Identifier:** Object ko identify aur retrieve karne ke liye uska key ya identifier.

Amazon S3 object storage ka example hai.

### Example
Agar aap S3 mein `photo.jpg` upload karti hain, to yeh file aik object ke taur par store hoti hai.

## 3. What Is an S3 Bucket?

### Definition
An S3 bucket is a container used to store objects in Amazon S3.

### Roman Urdu Explanation
Bucket ko aap cloud mein aik container ya folder jaisa samajh sakti hain jahan aap apni files store karti hain.

Technically, bucket aur normal computer folder mein farq hai. S3 objects ko bucket ke andar object keys ke zariye organize karta hai.

### Example
Aik bucket ka naam ho sakta hai:

`zahra-cloud-learning-2026`

Is bucket mein aap yeh objects rakh sakti hain:

- `images/photo.jpg`
- `documents/notes.pdf`
- `backups/database-backup.zip`

### Important Bucket Naming Rules

- Bucket name globally unique hona chahiye within the applicable AWS partition.
- Bucket name lowercase letters, numbers, hyphens aur kuch doosray permitted characters par mushtamil ho sakta hai.
- Simple aur meaningful name choose karein.
- Bucket name mein sensitive information, jaise passwords ya personal details, na likhein.
- Bucket name create karne se pehle AWS ki current naming rules check karein.

## 4. What Is an S3 Object?

### Definition
An S3 object is an individual piece of data stored inside an S3 bucket.

### Roman Urdu Explanation
S3 object woh actual file ya data hota hai jo bucket mein upload kiya jata hai.

Object ke andar data, metadata aur object key hoti hai.

### Examples of Objects

- `photo.jpg`
- `assignment.pdf`
- `video.mp4`
- `backup.zip`
- `index.html`

### What Is an Object Key?

Object key woh complete name hota hai jis se bucket ke andar object ko identify kiya jata hai.

Example:

`images/photo.jpg`

Is example mein `images/photo.jpg` object key hai.

Note: S3 mein `images/` aam tor par key ka aik prefix hota hai. Yeh lazmi nahi ke asal computer folder ki tarah exist karta ho.

## 5. Amazon S3 Storage Classes

### Definition
S3 storage classes are different storage options designed for different access patterns, availability needs, and costs.

### Roman Urdu Explanation
AWS mukhtalif storage classes provide karta hai. Har class ka use data ki access frequency aur storage requirements ke mutabiq hota hai.

### Common S3 Storage Classes

**1. S3 Standard**

Frequently accessed data ke liye use hoti hai.

Example: Aisi files jinhein application rozana use karti ho.

**2. S3 Intelligent-Tiering**

Aise data ke liye jo kabhi frequently aur kabhi infrequently access hota ho. AWS monitoring ke mutabiq data ko suitable access tiers mein move kar sakta hai.

Example: Aisi files jinki access frequency pehle se predict karna mushkil ho.

**3. S3 Standard-IA (Infrequent Access)**

Aise data ke liye jo kam access hota ho lekin zaroorat par relatively quickly available hona chahiye.

Example: Kabhi kabhi access kiye jane wale backups.

**4. S3 One Zone-IA**

Infrequently accessed data ke liye jo aik Availability Zone mein store hota hai.

Example: Aisi secondary copies jinhein dobara create kiya ja sakta ho.

Important: Is class mein aik Availability Zone ke loss se data availability ka risk zyada ho sakta hai.

**5. S3 Glacier Instant Retrieval**

Archive data ke liye jise kabhi kabhi access karna hota hai aur rapid retrieval ki zaroorat hoti hai.

**6. S3 Glacier Flexible Retrieval**

Archive data ke liye jahan retrieval time mein flexibility ho sakti hai.

**7. S3 Glacier Deep Archive**

Long-term archive data ke liye jo bohat kam access hota hai aur jise retrieve karne ke liye zyada intezar acceptable ho.

### Storage Class Selection

- Frequently used files: S3 Standard.
- Changing access patterns: S3 Intelligent-Tiering.
- Infrequently accessed data: suitable IA class.
- Long-term archives: suitable Glacier class.

Storage cost ke sath retrieval charges, request charges aur data transfer costs bhi check karein. Storage class choose karte waqt apni requirements aur current AWS pricing ko dekhna zaroori hai.

## 6. What Is S3 Versioning?

### Definition
S3 Versioning is a feature that keeps multiple versions of an object in a bucket.

### Roman Urdu Explanation
Versioning enable karne se aik hi object ki multiple versions save ho sakti hain.

Agar aap kisi file ko dobara upload karti hain, to purani version bhi retain ho sakti hai. Is se accidental overwrites ya deletions ke baad recovery mein help mil sakti hai.

### Example
Aap `notes.pdf` upload karti hain.

- Version 1: Original notes.
- Version 2: Updated notes.
- Version 3: Final notes.

Versioning ke zariye purani versions retrieve ki ja sakti hain, agar woh delete ya permanently remove na ki gayi hon.

### Benefits of Versioning

- Accidental overwrites se recovery mein help.
- Object ki previous versions retain karna.
- Data protection improve karna.
- Recovery options provide karna.

Important: Versioning backup strategy ka useful hissa hai, lekin yeh akelay har qisam ke data loss se protection guarantee nahi karta. Purani versions bhi storage cost leti hain.

## 7. What Is S3 Lifecycle Management?

### Definition
S3 Lifecycle Management uses rules to automatically transition objects between storage classes or expire objects according to defined conditions.

### Roman Urdu Explanation
Lifecycle rules ki madad se AWS ko bataya ja sakta hai ke purani files ko kab doosri storage class mein move karna hai ya kab expire karna hai.

### Example
Aap policy configure kar sakti hain ke purani files ko kuch waqt baad archive storage mein move kiya jaye.

Lifecycle rule apply karne se pehle ensure karein ke data ki recovery aur retention requirements poori ho rahi hain.

### Benefits

- Storage costs manage karna.
- Old data ko archive karna.
- Data retention policies implement karna.
- Unnecessary data ko policy ke mutabiq expire karna.

## 8. What Is S3 Bucket Policy?

### Definition
An S3 bucket policy is a resource-based AWS policy written in JSON that controls access to a bucket and its objects.

### Roman Urdu Explanation
Bucket policy aik JSON document hoti hai jo define karti hai ke kaun bucket ya uske objects par kaun se actions perform kar sakta hai.

Policy mein principals, actions, resources aur conditions specify ki ja sakti hain.

### Common Policy Elements

- **Effect:** Allow ya Deny.
- **Principal:** Kis identity ya account par policy apply hoti hai.
- **Action:** Kaun sa operation allowed ya denied hai.
- **Resource:** Kis bucket ya object par policy apply hoti hai.
- **Condition:** Kin conditions mein rule apply hoga.

### Important Security Rule
Bucket ko public karna sirf tab karein jab actual requirement ho. Public access se files unauthorized users ko accessible ho sakti hain.

Private storage ke liye public access block settings enabled rakhna aam tor par behtar hai.

## 9. What Is Block Public Access?

### Definition
Amazon S3 Block Public Access provides settings that help prevent public access to buckets and objects.

### Roman Urdu Explanation
Block Public Access S3 ki security feature hai jo accidental public exposure ko rokne mein help karti hai.

Agar aap sirf apni private files store karna chahti hain, to public access ki zaroorat nahi hoti.

Is liye public access block settings ko enabled rakhna aik important security practice hai.

### Best Practices

- Unnecessary public access enable na karein.
- Bucket policies ko carefully review karein.
- IAM permissions ko minimum required access tak limit karein.
- Sensitive files ko public links ke zariye share na karein.
- Public website ya data sharing ke liye approved aur secure configuration use karein.

## 10. What Is IAM in Amazon S3?

### Definition
AWS Identity and Access Management (IAM) helps control which identities can access AWS services and perform actions.

### Roman Urdu Explanation
IAM ki madad se hum users, roles aur doosri identities ki permissions control karte hain.

Example: Aik IAM user ko S3 objects read karne ki permission di ja sakti hai, lekin bucket delete karne ki permission na di jaye.

### Principle of Least Privilege

Least Privilege ka matlab hai ke user ya application ko sirf utni permissions di jayein jitni uske kaam ke liye zaroori hain.

Example: Agar application ko sirf aik bucket se files read karni hain, to usay tamam AWS resources ka full access dena zaroori nahi.

## 11. What Is Server-Side Encryption?

### Definition
Server-side encryption is a method in which data is encrypted at rest by the service storing it.

### Roman Urdu Explanation
Amazon S3 mein server-side encryption data ko storage mein encrypted form mein rakhne mein help karti hai.

S3 mein different encryption options available hain, jin mein Amazon S3 managed keys aur AWS Key Management Service (AWS KMS) ke sath encryption shamil hain.

### Why Is Encryption Important?

- Stored data ki confidentiality improve hoti hai.
- Unauthorized access ke risk ko kam karne mein help milti hai.
- Security aur compliance requirements support ho sakti hain.

Encryption access control ka replacement nahi hai. IAM aur bucket permissions ko bhi properly configure karna zaroori hai.

## 12. What Is Static Website Hosting on S3?

### Definition
Amazon S3 can host static website content, such as HTML, CSS, JavaScript, and images, through its static website hosting feature.

### Roman Urdu Explanation
Aap S3 mein website ki static files upload kar sakti hain. Misal ke taur par HTML, CSS aur images.

Static website ka matlab hai ke website content S3 se serve hota hai. Traditional server-side code, jaise PHP ya Python application logic, S3 static website hosting se directly execute nahi hota.

### Examples

- Personal portfolio.
- Simple HTML website.
- Course project website.
- Static documentation website.

### Important Security Note
S3 website endpoint aam tor par HTTPS provide nahi karta. Secure HTTPS delivery ke liye Amazon CloudFront jaisi service use ki ja sakti hai.

Public website hosting mein access configuration carefully plan karein. Agar website files public honi chahiye, to sirf required content ko public access dene ka approved tareeqa use karein.

## 13. Practical Lab — Create an S3 Bucket

### Lab Objective
Is lab mein hum AWS Console ke zariye aik S3 bucket create karenge aur us mein aik file upload karenge.

### Step 1: Sign In to AWS

1. AWS Management Console open karein.
2. Apne AWS account mein sign in karein.
3. Services mein Amazon S3 search karein.
4. S3 service open karein.

### Step 2: Create a Bucket

1. Create bucket par click karein.
2. Bucket name enter karein, example:

`zahra-s3-learning-2026-unique`

Note: Is naam ko zaroorat ke mutabiq change karein. Agar naam pehle se kisi aur ke paas hai, to doosra globally unique naam choose karein.

3. Apni required AWS Region select karein.
4. General-purpose bucket ki default settings ko review karein.
5. Block Public Access settings enabled rakhein.
6. Create bucket par click karein.

### Step 3: Upload a File

1. Apni newly created bucket open karein.
2. Upload par click karein.
3. Add files par click karein.
4. Computer se koi sample file select karein.
5. Upload par click karein.

### Step 4: Verify the Object

1. Bucket ke Objects tab mein jayein.
2. Uploaded file ka naam check karein.
3. File ki details open karein.
4. Object ka naam, size aur doosri available information verify karein.

### Step 5: Test Private Access

Bucket private ho to sirf URL open karne se har user ko file access nahi milega.

Authorized access ke liye AWS Console, suitable IAM permissions, ya approved access method use karein.

Agar aap public access enable nahi karna chahti, to sirf file test karne ke liye bucket ko public na karein.

### Step 6: Delete the Test Object and Bucket

Lab complete hone ke baad:

1. Sample object select karein.
2. Delete par click karein.
3. Confirmation ke liye required text enter karein.
4. Object delete karein.
5. Agar bucket ki zaroorat nahi rahi, to bucket ko empty karke delete karein.

Important: Bucket delete karne se pehle confirm karein ke us mein koi important data nahi hai. Versioning enabled ho to purani object versions aur delete markers ko bhi manage karna par sakta hai.

## 14. Basic AWS CLI Commands for S3

AWS CLI use karne ke liye AWS CLI installed aur credentials ya role properly configured hona chahiye.

### Check AWS Identity

```bash
aws sts get-caller-identity
```

Yeh configured AWS identity ki information show karta hai.

### List S3 Buckets

```bash
aws s3 ls
```

Yeh accessible S3 buckets list karne ki koshish karta hai.

### Create a Bucket

Example for a chosen Region:

```bash
aws s3api create-bucket --bucket YOUR-UNIQUE-BUCKET-NAME --region us-east-1
```

`YOUR-UNIQUE-BUCKET-NAME` ko apne unique bucket name se replace karein.

Note: Yeh example `us-east-1` ke liye hai. Doosri Regions mein bucket create karte waqt required Region-specific parameters different ho sakte hain.

### Upload a File

```bash
aws s3 cp notes.pdf s3://YOUR-UNIQUE-BUCKET-NAME/
```

Yeh local `notes.pdf` file ko specified bucket mein upload karta hai.

### List Objects

```bash
aws s3 ls s3://YOUR-UNIQUE-BUCKET-NAME/
```

Yeh bucket ke objects list karta hai, agar aapke paas required permissions hon.

### Download a File

```bash
aws s3 cp s3://YOUR-UNIQUE-BUCKET-NAME/notes.pdf downloaded-notes.pdf
```

Yeh S3 se file download karke local machine par `downloaded-notes.pdf` naam se save karta hai.

### Delete an Object

```bash
aws s3 rm s3://YOUR-UNIQUE-BUCKET-NAME/notes.pdf
```

Yeh specified object delete karne ki request karta hai, agar permissions allow karti hon.

Warning: Versioning enabled ho to delete operation ka behavior different ho sakta hai. Important data par commands run karne se pehle object aur bucket name carefully verify karein.

## 15. Common S3 Errors

### AccessDenied
Iska matlab hai ke current identity ke paas required action ki permission nahi hai, ya koi applicable policy access restrict kar rahi hai.

Solution:
- IAM permissions check karein.
- Bucket policy review karein.
- Organization policies aur encryption permissions bhi check karein, agar applicable hon.

### BucketAlreadyExists
Bucket ka naam globally available nahi hai.

Solution: Doosra unique bucket name choose karein.

### NoSuchBucket
Specified bucket nahi mil rahi ya bucket name/Region incorrect ho sakta hai.

Solution:
- Bucket name verify karein.
- Region check karein.
- Confirm karein ke bucket exist karti hai.

### File Is Not Publicly Accessible
Agar file public nahi hai, to browser se direct URL open karne par access error aa sakta hai.

Solution: File ko public banane se pehle requirement aur security review karein. Private file ke liye authenticated access ya approved presigned URL use kiya ja sakta hai.

## 16. Amazon S3 Security Best Practices

1. Public access block settings enabled rakhein jab public access required na ho.
2. IAM mein least privilege follow karein.
3. Sensitive data ke liye encryption requirements verify karein.
4. Versioning ko important data ke liye consider karein.
5. Lifecycle rules se data retention aur storage costs manage karein.
6. Bucket policies ko carefully review karein.
7. AWS access keys ko GitHub par upload na karein.
8. Application credentials ko securely manage karein.
9. Important data ke liye suitable backup aur recovery plan banayein.
10. AWS costs aur storage usage monitor karein.
11. Sensitive data ke liye access logging aur monitoring requirements evaluate karein.
12. Bucket mein unnecessary files store na karein.

## 17. Important Interview Questions

### Q1. What is Amazon S3?
Amazon S3 is an AWS object storage service used to store, retrieve, and manage data.

### Q2. What is an S3 bucket?
An S3 bucket is a container used to store objects.

### Q3. What is an S3 object?
An S3 object is an individual piece of data stored in a bucket.

### Q4. What is an object key?
An object key uniquely identifies an object within its bucket.

### Q5. What is S3 Versioning?
S3 Versioning keeps multiple versions of an object to help recover from accidental overwrites or deletions.

### Q6. What is S3 Lifecycle Management?
It uses rules to transition objects between storage classes or expire objects.

### Q7. What is a bucket policy?
A bucket policy is a JSON-based resource policy that controls access to a bucket and its objects.

### Q8. What is Block Public Access?
It is a group of S3 settings that helps prevent public access to buckets and objects.

### Q9. What is S3 server-side encryption?
It is a feature that encrypts data at rest in Amazon S3.

### Q10. What is S3 static website hosting?
It is a feature that serves static website files, such as HTML, CSS, JavaScript, and images.

### Q11. What is the principle of least privilege?
It means giving an identity only the permissions required to perform its tasks.

### Q12. Can Amazon S3 store videos and images?
Yes. Amazon S3 can store many types of files, including videos, images, documents, backups, and logs.

## 18. Class Summary

- Amazon S3 is an AWS object storage service.
- Buckets are containers used to store objects.
- Objects contain data, metadata, and an object key.
- S3 provides different storage classes for different access patterns.
- Versioning helps retain and recover object versions.
- Lifecycle rules help automate storage transitions and expiration.
- Bucket policies and IAM control access.
- Block Public Access helps prevent accidental public exposure.
- Server-side encryption protects stored data.
- S3 can host static website files.
- AWS CLI can upload, download, list, and delete objects.
- Security, permissions, data recovery, and cost management are important when using S3.
