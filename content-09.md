
# Class 9 — AWS aur IAM (Identity and Access Management)

## 1. What Is AWS?

### Definition
Amazon Web Services (AWS) is a cloud computing platform that provides computing, storage, networking, databases, security, and other IT services over the internet.

### Roman Urdu Explanation
AWS Amazon ki cloud computing service hai. Iski madad se hum internet ke zariye servers, storage, databases aur networking services use kar sakte hain.

Pehle kisi company ko server use karne ke liye physical computer khareedna, usay install karna aur maintain karna parta tha. AWS ki madad se company cloud mein resources create karke apni requirements ke mutabiq use kar sakti hai.

### Real-Life Example
Agar aap aik website banana chahti hain, to AWS par:

- EC2 se virtual server create kar sakti hain.
- S3 mein website ki files store kar sakti hain.
- IAM se users aur permissions manage kar sakti hain.
- VPC se network environment configure kar sakti hain.
- CloudWatch se resources monitor kar sakti hain.

### Benefits of AWS

- Scalability: Zaroorat ke mutabiq resources increase ya decrease karna.
- Flexibility: Mukhtalif services ko apni requirement ke mutabiq use karna.
- Global Infrastructure: Mukhtalif geographical locations mein AWS infrastructure use karna.
- Security Tools: Identity, access control, encryption aur monitoring ke tools.
- Pay-as-you-go: Kai services mein usage ke mutabiq payment hoti hai.

Important: AWS ki services free ya paid ho sakti hain. Charges service, configuration aur usage par depend karte hain.

## 2. What Is IAM?

### Definition
AWS Identity and Access Management (IAM) is a service that helps securely control access to AWS resources by managing identities, permissions, and authentication.

### Roman Urdu Explanation
IAM ka full form Identity and Access Management hai.

AWS IAM aik security service hai jo control karti hai ke kaun AWS account mein sign in kar sakta hai aur kaun se AWS resources par kaun se actions perform kar sakta hai.

Misal ke taur par, aik student ko S3 ki files dekhne ki permission di ja sakti hai, lekin usay EC2 instances delete karne ki permission na di jaye.

IAM ka main maqsad yeh hai ke har identity ko sirf required access diya jaye.

### Why Is IAM Important?

- AWS resources ko secure rakhna.
- Users ki permissions control karna.
- Unauthorized access ko rokne mein help karna.
- Different users ko different responsibilities dena.
- Applications ko AWS resources tak controlled access dena.
- Security policies implement karna.

### Real-Life Example
Aik college mein principal, teacher aur student ke access rights different hote hain.

- Principal ko administrative access mil sakta hai.
- Teacher ko class records access karne ki permission mil sakti hai.
- Student ko sirf apna learning material dekhne ki permission mil sakti hai.

Isi tarah AWS IAM mein different identities ko different permissions di jati hain.

## 3. Main Components of IAM

AWS IAM ke important components yeh hain:

1. IAM Users
2. IAM Groups
3. IAM Roles
4. IAM Policies
5. Authentication
6. Authorization
7. Multi-Factor Authentication (MFA)

Har component ka apna role hai.

## 4. What Is an IAM User?

### Definition
An IAM user is an identity in an AWS account that can be assigned permissions to access AWS resources.

### Roman Urdu Explanation
IAM user aik identity hoti hai jo AWS account ke andar create ki jati hai. Is user ko required permissions di ja sakti hain.

Agar kisi employee ko AWS Console use karna ho ya kisi specific task ke liye access chahiye ho, to uske liye IAM user create kiya ja sakta hai, jab yeh organization ke access model ke mutabiq ho.

IAM user ke sath console password ya programmatic access credentials configure kiye ja sakte hain. Har user ko dono ki zaroorat nahi hoti.

### Example
Aik AWS account mein yeh IAM users ho sakte hain:

- `developer-user`
- `testing-user`
- `security-user`

Har user ki permissions uske kaam ke mutabiq configure ki ja sakti hain.

### Important Security Points

- Har user ko sirf required permissions dein.
- Password aur access keys share na karein.
- MFA enable karein.
- Unused credentials ko remove ya deactivate karein.
- Long-term access keys ko unnecessary use na karein.

Note: AWS mein human users ke liye federated access aur IAM Identity Center aksar preferred options hote hain. IAM users har situation mein zaroori nahi.

## 5. What Is an IAM Group?

### Definition
An IAM group is a collection of IAM users that can share common permissions through policies attached to the group.

### Roman Urdu Explanation
IAM group multiple IAM users ka collection hota hai. Is se similar responsibilities wale users ko common permissions dena easy ho jata hai.

### Example
Aik company mein 5 developers hain. Agar sab ko same development permissions deni hain, to developers ka group banaya ja sakta hai aur suitable policy attach ki ja sakti hai.

### Example Groups

- `Developers`
- `Administrators`
- `Auditors`
- `ReadOnlyUsers`

### Benefits of IAM Groups

- Permissions manage karna easy hota hai.
- Users ko common access diya ja sakta hai.
- Repeated policy assignment kam hoti hai.
- Access management zyada organized ho jati hai.

Important: IAM groups mein users ho sakte hain, lekin IAM roles groups ke andar add nahi kiye jate.

## 6. What Is an IAM Role?

### Definition
An IAM role is an AWS identity with permissions that can be assumed by an authorized user, application, AWS service, or other trusted principal.

### Roman Urdu Explanation
IAM role aik identity hoti hai jiske sath permissions attached hoti hain. Authorized identity ya service role assume karke uski permissions ke mutabiq kaam kar sakti hai.

Roles temporary security credentials provide kar sakte hain. Is wajah se applications ko long-term access keys dene ki zaroorat kam ho sakti hai.

### Real-Life Example
Aik EC2 instance ko S3 se file download karni hai.

Har baar application ke andar access key aur secret key save karne ke bajaye, EC2 instance ke sath suitable IAM role attach kiya ja sakta hai.

Agar role ko required S3 permissions di gayi hon, to application temporary credentials use karke authorized files access kar sakti hai.

### Common Uses of IAM Roles

- EC2 applications ko AWS access dena.
- Lambda functions ko AWS resources access karwana.
- Cross-account access configure karna.
- Federated users ko AWS access dena.
- AWS services ko required actions perform karne dena.

### IAM User vs IAM Role

| IAM User | IAM Role |
|---|---|
| AWS account mein user identity hoti hai | Assume ki jane wali identity hoti hai |
| Password ya access keys ho sakti hain | Aksar temporary credentials use hote hain |
| Human ya specific identity ke liye use ho sakta hai | Users, applications aur services assume kar sakte hain |
| Long-term credentials ka risk ho sakta hai | Temporary credentials access ko manage karne mein help karte hain |

## 7. What Is an IAM Policy?

### Definition
An IAM policy is a JSON document that defines permissions by specifying which actions are allowed or denied on which resources and under what conditions.

### Roman Urdu Explanation
IAM policy aik JSON document hota hai jo define karta hai ke kisi identity ko AWS mein kya karne ki permission hai aur kis resource par hai.

Policy mein yeh define kiya ja sakta hai ke user files read kar sakta hai, files upload kar sakta hai ya kisi resource ko delete kar sakta hai.

### Main Elements of an IAM Policy

**1. Version**

Policy language ka version define karta hai.

**2. Statement**

Policy ke permission rules contain karta hai.

**3. Effect**

Batata hai ke action `Allow` hai ya `Deny`.

**4. Action**

AWS operation define karta hai, jaise `s3:ListBucket`.

**5. Resource**

Batata hai ke permission kis AWS resource par apply hoti hai.

**6. Condition**

Optional conditions define karti hai jin ke mutabiq policy apply hoti hai.

### Example of an IAM Policy

Yeh example aik specific S3 bucket ko list karne aur us bucket ke objects read karne ki permission deta hai.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::my-example-bucket"
    },
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-example-bucket/*"
    }
  ]
}
```

Important: `my-example-bucket` ko apni actual bucket ke naam se replace karein. Yeh policy bucket ke objects read karne aur list karne ki permission deti hai; upload ya delete ki permission nahi deti.

### What Is an ARN?

ARN ka full form Amazon Resource Name hai.

ARN AWS resources ko uniquely identify karne ke liye use hota hai.

Example:

`arn:aws:s3:::my-example-bucket`

Yeh example aik S3 bucket ko identify karta hai.

### Types of IAM Policies

**1. AWS Managed Policies**

AWS ke banaye hue policies jinhein AWS maintain karta hai.

**2. Customer Managed Policies**

Customer apni requirements ke mutabiq create aur manage karta hai.

**3. Inline Policies**

Aik specific IAM identity ke sath directly attached policy.

Policy ka selection least privilege aur actual requirements ke mutabiq hona chahiye.

## 8. What Is Authentication?

### Definition
Authentication is the process of verifying the identity of a user or system.

### Roman Urdu Explanation
Authentication ka matlab hai verify karna ke aap waqai wohi user hain hone ka claim kar rahi hain.

### Example
Jab aap AWS Console mein username aur password enter karti hain aur AWS aapki identity verify karta hai, to yeh authentication hai.

Authentication ke methods mein passwords, MFA aur federated sign-in shamil ho sakte hain.

## 9. What Is Authorization?

### Definition
Authorization determines which actions an authenticated identity is permitted to perform.

### Roman Urdu Explanation
Authorization ka matlab hai decide karna ke verified user ko kya karne ki permission hai.

### Example
Aap AWS mein sign in kar leti hain, lekin aapke paas EC2 instance delete karne ki permission nahi hai.

Aapki identity verify ho gayi, yani authentication complete ho gayi. Lekin delete action allowed hai ya nahi, yeh authorization ka hissa hai.

### Authentication vs Authorization

| Authentication | Authorization |
|---|---|
| Identity verify karta hai | Permissions determine karta hai |
| Aap kaun hain? | Aap kya kar sakte hain? |
| Example: Sign-in verification | Example: S3 object delete karne ki permission |

## 10. What Is the Principle of Least Privilege?

### Definition
The principle of least privilege means granting only the minimum permissions required to perform a specific task.

### Roman Urdu Explanation
Least privilege ka matlab hai kisi user, application ya service ko sirf utna access dena jitna uske kaam ke liye zaroori hai.

Har user ko Administrator access dena secure practice nahi hai.

### Example
Agar kisi employee ko sirf S3 files read karni hain, to usay poore AWS account ka full access dene ke bajaye sirf required S3 read permissions di jani chahiye.

### Benefits

- Unauthorized actions ka risk kam hota hai.
- Accidental deletion ka risk kam hota hai.
- Security improve hoti hai.
- Access audit karna easy hota hai.

## 11. What Is Multi-Factor Authentication (MFA)?

### Definition
Multi-Factor Authentication (MFA) requires additional verification beyond a password to help verify a user's identity.

### Roman Urdu Explanation
MFA aik extra security layer hai. Is mein password ke ilawa aik aur verification factor use hota hai.

Agar kisi ko password pata bhi chal jaye, to additional verification ki wajah se account ki security improve ho sakti hai.

### Examples of MFA Methods

- Authenticator application.
- Hardware security key.
- AWS-supported security authentication method.

### Why Is MFA Important?

- Account security improve hoti hai.
- Stolen passwords ke risk ko reduce karne mein help milti hai.
- Important AWS accounts ko protect karne mein help karta hai.

### Best Practice

Root user aur privileged administrative access ke liye MFA enable karein. Organization ki requirements ke mutabiq strong authentication methods choose karein.

## 12. What Is the AWS Root User?

### Definition
The AWS account root user is the identity created when an AWS account is established. It has extensive permissions and is not restricted by ordinary IAM identity policies in the same way as IAM users and roles.

### Roman Urdu Explanation
AWS root user account ki original identity hoti hai. Is ke paas bohat powerful permissions hoti hain.

Root user ko routine tasks ke liye use karna avoid karna chahiye.

### Root User Security Best Practices

1. Root user par MFA enable karein.
2. Root credentials kisi ke sath share na karein.
3. Root user ki access details secure rakhein.
4. Daily AWS work ke liye suitable IAM role ya authorized user access use karein.
5. Root user ki access keys create na karein jab tak koi exceptional, justified requirement na ho.

Important: Kuch account-level tasks root user ke liye required ho sakte hain. Root access ko carefully manage karein.

## 13. What Is AWS STS?

### Definition
AWS Security Token Service (AWS STS) provides temporary security credentials for authorized access to AWS resources.

### Roman Urdu Explanation
AWS STS temporary security credentials provide karta hai. Yeh credentials limited duration ke liye use kiye ja sakte hain.

IAM roles aur federated access mein temporary credentials bohat important hain.

### Benefits

- Long-term access keys par dependence kam karna.
- Temporary access provide karna.
- Cross-account access support karna.
- AWS resources ko controlled access dena.

## 14. What Is an Access Key?

### Definition
An AWS access key is a credential pair used to authenticate programmatic requests to AWS services.

### Roman Urdu Explanation
Access key ka use applications aur command-line tools ko AWS services ke sath authenticate karne ke liye kiya ja sakta hai.

Access key ID aur secret access key credential pair ka hissa hain.

### Security Rules

- Secret access key ko password ki tarah protect karein.
- Access keys GitHub par upload na karein.
- Keys ko messages ya public repositories mein share na karein.
- Unused keys ko deactivate ya delete karein.
- Jahan possible ho, IAM roles aur temporary credentials use karein.

## 15. What Is IAM Identity Center?

### Definition
AWS IAM Identity Center is a service for centrally managing workforce access to AWS accounts and supported applications.

### Roman Urdu Explanation
IAM Identity Center organization ke employees ko centrally manage kiye gaye access ke zariye AWS accounts aur applications tak access dene mein help karta hai.

Organizations mein har employee ke liye alag long-term credentials manage karne ke bajaye centralized sign-in aur permission assignment use ki ja sakti hai.

## 16. Practical Lab — Create an IAM User

### Lab Objective
Is lab mein hum AWS Console mein IAM user create karna, limited permissions assign karna aur access ko verify karna seekhenge.

Important: AWS account ki organization policy follow karein. Human users ke liye IAM Identity Center ya federated access preferred ho sakta hai. Yeh lab educational purpose ke liye hai.

### Step 1: Sign In to AWS

1. AWS Management Console open karein.
2. Apne authorized AWS account mein sign in karein.
3. Search bar mein IAM type karein.
4. IAM service open karein.

### Step 2: Open Users

1. IAM navigation menu mein Users select karein.
2. Create user par click karein.
3. Username enter karein, example:

`student-lab-user`

4. Console access ki requirement ho to appropriate option select karein.
5. Organization ki password aur authentication policies follow karein.
6. Next par click karein.

### Step 3: Assign Permissions

Learning purpose ke liye aap suitable limited-access policy select kar sakti hain.

Example: Sirf read-only learning ki requirement ho to suitable read-only policy consider karein.

AdministratorAccess sirf tab use karein jab authorized administrative task ke liye waqai zaroori ho.

### Step 4: Review and Create

1. Username verify karein.
2. Permissions carefully review karein.
3. Create user par click karein.
4. User ki configuration verify karein.

### Step 5: Enable MFA

Agar user console access use karta hai, to supported MFA method configure karein.

1. IAM mein user open karein.
2. Security credentials ya MFA section open karein.
3. Assign MFA device select karein.
4. Supported method ke instructions follow karein.
5. Setup complete hone ke baad MFA verify karein.

### Step 6: Test Permissions

User ko sirf wahi AWS actions perform karne chahiye jo uski policies allow karti hain.

Agar user ko kisi action ki permission nahi hai, to AWS access-denied error return kar sakta hai.

### Step 7: Clean Up the Lab

Lab complete hone ke baad:

1. Test user ki requirement review karein.
2. Unnecessary console access disable karein.
3. Unused access keys deactivate ya delete karein.
4. Temporary test identities ko organization policy ke mutabiq remove karein.

## 17. Practical Lab — Create an IAM Role for EC2

### Lab Objective
EC2 instance ko IAM role ke zariye AWS resources ka limited access dena.

### Step 1: Open IAM Roles

1. AWS Console mein IAM open karein.
2. Roles select karein.
3. Create role par click karein.

### Step 2: Select Trusted Entity

1. AWS service select karein.
2. Use case mein EC2 choose karein.
3. Next par click karein.

### Step 3: Attach Permissions

Sirf required policy select karein.

Example: Agar EC2 application ko aik specific S3 bucket se files read karni hain, to usi bucket aur required read actions tak limited policy use karein.

Full S3 access ya AdministratorAccess dene se avoid karein jab tak actual requirement na ho.

### Step 4: Name and Create the Role

Role ka naam rakhein:

`EC2-S3-ReadOnly-Lab-Role`

Role ki trust relationship aur permissions review karein. Phir role create karein.

### Step 5: Attach the Role to EC2

1. EC2 Console open karein.
2. Instance select karein.
3. Actions ya Security menu mein Modify IAM role option locate karein.
4. Created role select karein.
5. Update ya Save par click karein.

### Step 6: Verify Access

EC2 instance ke andar configured AWS SDK ya CLI se required S3 operation test karein, agar tools installed aur access configured ho.

Application ko static access keys dene ke bajaye instance role ki temporary credentials use karni chahiye.

## 18. Useful AWS CLI Commands

AWS CLI commands run karne ke liye AWS CLI installed aur credentials ya role properly configured hona chahiye.

### Check Current AWS Identity

```bash
aws sts get-caller-identity
```

Yeh configured identity aur account ki information return karta hai.

### List IAM Users

```bash
aws iam list-users
```

Yeh IAM users list karta hai, agar current identity ke paas permission ho.

### List IAM Roles

```bash
aws iam list-roles
```

Yeh IAM roles list karta hai, agar required permission available ho.

### List Attached User Policies

```bash
aws iam list-attached-user-policies --user-name student-lab-user
```

Yeh specified IAM user ke sath attached managed policies list karta hai.

### Check AWS CLI Version

```bash
aws --version
```

Yeh installed AWS CLI version show karta hai.

Important: IAM commands ko sirf authorized AWS account mein run karein. Unnecessary permissions add karne ya production identities modify karne se pehle impact review karein.

## 19. Common IAM Errors

### AccessDenied

Iska matlab hai ke requested action allowed nahi hai ya kisi applicable policy ne access restrict kiya hai.

Possible reasons:
- Required permission missing hai.
- Resource policy access restrict kar rahi hai.
- Explicit Deny applicable hai.
- Organization-level policy ya permissions boundary restriction apply ho rahi hai.

### InvalidClientTokenId

Configured security token ya access key invalid ho sakti hai.

Possible checks:
- Credentials correct hain ya nahi.
- Expired temporary credentials ko refresh kiya gaya hai ya nahi.
- AWS CLI profile correct hai ya nahi.

### ExpiredToken

Temporary credentials expire ho chuki hain.

Solution: Authorized sign-in ya role-assumption process ke zariye fresh credentials hasil karein.

### MFA Verification Problem

MFA code ya device configuration mein issue ho sakta hai.

Solution:
- Device aur current code verify karein.
- Time synchronization check karein, agar relevant ho.
- Authorized account recovery process follow karein.

## 20. Important IAM Security Best Practices

1. Root user ko routine tasks ke liye use na karein.
2. Root user aur privileged users par MFA enable karein.
3. Least privilege follow karein.
4. Applications ke liye IAM roles ko prefer karein.
5. Long-term access keys ko unnecessary use na karein.
6. Passwords aur secret keys ko secure rakhein.
7. AWS credentials GitHub repository mein upload na karein.
8. Unused users, roles aur credentials review karein.
9. Policies mein `Action: "*"` aur `Resource: "*"` ko avoid karein jab tak justified na hon.
10. IAM permissions ko regularly review karein.
11. CloudTrail ke zariye relevant account activity monitor karein.
12. Organization ki security aur access policies follow karein.

## 21. Important Interview Questions

### Q1. What is AWS IAM?
AWS IAM is a service that manages identities and controls access to AWS resources.

### Q2. What is an IAM user?
An IAM user is an identity in an AWS account that can be assigned permissions.

### Q3. What is an IAM group?
An IAM group is a collection of IAM users that can share common permissions.

### Q4. What is an IAM role?
An IAM role is an identity with permissions that an authorized principal can assume.

### Q5. What is an IAM policy?
An IAM policy is a document that defines allowed or denied actions on resources.

### Q6. What is least privilege?
Least privilege means granting only the minimum permissions required for a task.

### Q7. What is MFA?
MFA is an authentication method that requires additional verification beyond a password.

### Q8. What is the AWS root user?
It is the original identity associated with an AWS account and has extensive account permissions.

### Q9. What is the difference between authentication and authorization?
Authentication verifies identity, while authorization determines what that identity can do.

### Q10. Why are IAM roles useful for EC2?
IAM roles allow EC2 applications to obtain temporary credentials for authorized AWS access without storing long-term access keys in the application.

### Q11. What is AWS STS?
AWS STS provides temporary security credentials for authorized AWS access.

### Q12. What is an ARN?
An Amazon Resource Name identifies an AWS resource.

### Q13. Why should AWS access keys not be uploaded to GitHub?
Publicly exposed credentials can be misused to access AWS resources and may cause data loss or unexpected charges.

### Q14. What is IAM Identity Center?
It helps centrally manage workforce access to AWS accounts and supported applications.

## 22. Class Summary

- AWS cloud computing services provide servers, storage, databases, and networking.
- IAM stands for Identity and Access Management.
- IAM helps manage identities and permissions.
- IAM users represent identities within an AWS account.
- IAM groups help assign common permissions to users.
- IAM roles provide permissions that authorized identities or services can assume.
- IAM policies define allowed and denied actions.
- Authentication verifies identity.
- Authorization determines permitted actions.
- Least privilege means giving only the required permissions.
- MFA adds another layer of authentication security.
- Root user access should be carefully protected.
- AWS STS provides temporary security credentials.
- IAM roles are useful for giving EC2 applications controlled AWS access.
- Strong IAM security helps protect AWS resources and data.
