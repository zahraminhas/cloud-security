
# Class 11 — IAM Policies in Depth (Writing a Keycard)

## 1. What Is an IAM Policy?

### Definition
An AWS IAM policy is a document that defines permissions by specifying which actions are allowed or denied on AWS resources and under what conditions.

### Roman Urdu Explanation
IAM policy aik JSON document hota hai jo AWS ko batata hai ke kisi user, group ya role ko kya karne ki permission hai aur kis resource par hai.

Misal ke taur par, agar kisi student ko sirf S3 bucket mein files dekhne ki permission deni ho, to hum aisi policy likh sakte hain jo files read karne de lekin delete karne ki permission na de.

### Real-Life Example: Keycard
Office mein keycard ke zariye employees ko different rooms ka access diya jata hai.

- Employee A sirf office mein enter kar sakta hai.
- Employee B office aur server room mein enter kar sakta hai.
- Administrator ko additional rooms ka access mil sakta hai.

AWS IAM policy bhi isi tarah access control karti hai. Policy define karti hai ke identity kaun se resources par kaun se actions perform kar sakti hai.

## 2. Why Are IAM Policies Important?

IAM policies AWS security ka important hissa hain.

### Main Purposes

1. AWS resources ka access control karna.
2. Users ko required permissions dena.
3. Unnecessary permissions ko restrict karna.
4. Applications ko AWS services ka controlled access dena.
5. Sensitive data ko protect karna.
6. Least Privilege principle implement karna.
7. Unauthorized actions ka risk kam karna.

### Example
Agar aik developer ko sirf aik S3 bucket se files read karni hain, to usay poore AWS account ka AdministratorAccess dena zaroori nahi.

Aik limited policy se developer ko required bucket aur required actions tak access diya ja sakta hai.

## 3. What Is JSON?

### Definition
JSON stands for JavaScript Object Notation. It is a text-based data format used to represent structured information.

### Roman Urdu Explanation
JSON aik format hai jisme data keys aur values ki form mein likha jata hai.

AWS IAM policies JSON format mein likhi jati hain.

### Simple JSON Example

```json
{
  "name": "Student",
  "course": "Cloud Security",
  "level": "Beginner"
}
```

Is example mein:
- `name` aik key hai.
- `Student` uski value hai.
- `course` aik key hai.
- `Cloud Security` uski value hai.

IAM policy mein bhi isi tarah fields ke zariye permissions define hoti hain.

## 4. Structure of an IAM Policy

### Definition
An IAM policy contains statements that describe the permissions granted or denied to a principal.

### Main Policy Elements

1. Version
2. Statement
3. Sid
4. Effect
5. Principal
6. Action
7. Resource
8. Condition

Har policy mein tamam elements hona zaroori nahi. Kuch elements policy ki type aur purpose ke mutabiq use hote hain.

## 5. What Is Version?

### Definition
The Version element specifies the version of the IAM policy language.

### Roman Urdu Explanation
`Version` batata hai ke policy kis IAM policy language version ko use kar rahi hai.

Common value:

```json
"Version": "2012-10-17"
```

Yeh IAM policy language ka version hai, policy banane ki date nahi.

## 6. What Is Statement?

### Definition
The Statement element contains one or more permission statements in an IAM policy.

### Roman Urdu Explanation
`Statement` policy ka woh hissa hai jahan permission rules likhe jate hain.

Aik policy mein aik ya multiple statements ho sakte hain.

Example:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListAllMyBuckets",
      "Resource": "*"
    }
  ]
}
```

Yeh example S3 buckets list karne ki permission deta hai, agar koi doosri applicable policy ya restriction is action ko block na kar rahi ho.

Note: `Resource: "*"` ka scope carefully samajhna zaroori hai. Least privilege ke liye jahan possible ho, resource access ko restrict karein.

## 7. What Is Sid?

### Definition
Sid stands for Statement ID. It is an optional identifier used to describe a policy statement.

### Roman Urdu Explanation
`Sid` statement ko aik meaningful naam ya identifier dene ke liye use hota hai.

Example:

```json
{
  "Sid": "AllowReadOnlyAccess"
}
```

Is se policy ko samajhna aur review karna easy ho sakta hai.

## 8. What Is Effect?

### Definition
The Effect element specifies whether a policy statement allows or denies an action.

### Roman Urdu Explanation
`Effect` batata hai ke policy rule kisi action ko allow karta hai ya deny.

Iski do common values hain:

- `Allow`
- `Deny`

### Allow Example

```json
{
  "Effect": "Allow"
}
```

Yeh statement action ko allow karne ke liye use hota hai.

### Deny Example

```json
{
  "Effect": "Deny"
}
```

Yeh statement action ko deny karne ke liye use hota hai.

### Important Rule
Applicable explicit `Deny` aam tor par `Allow` par precedence rakhta hai.

Iska matlab hai ke agar aik policy action allow karti hai aur doosri applicable policy usi action ko explicitly deny karti hai, to action deny hota hai.

## 9. What Is Action?

### Definition
The Action element specifies the AWS API operations that a policy statement allows or denies.

### Roman Urdu Explanation
`Action` batata hai ke user ya role AWS mein kaun sa kaam kar sakta hai.

Examples:

- `s3:ListBucket` — bucket ke objects list karna.
- `s3:GetObject` — object read ya download karna.
- `s3:PutObject` — object upload karna.
- `s3:DeleteObject` — object delete karna.
- `ec2:DescribeInstances` — EC2 instances ki information dekhna.

### Example

```json
{
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::my-example-bucket/*"
}
```

Yeh statement specified bucket ke objects read karne ki permission deta hai.

Important: Sirf `s3:GetObject` se bucket ke objects list karne ki permission nahi milti. Listing ke liye aksar `s3:ListBucket` ki bhi zaroorat hoti hai.

## 10. What Is Resource?

### Definition
The Resource element specifies the AWS resources to which a policy statement applies.

### Roman Urdu Explanation
`Resource` batata hai ke permission kis AWS resource par apply hogi.

AWS resources ko identify karne ke liye ARN use hota hai.

### What Is ARN?

ARN ka full form Amazon Resource Name hai.

Example:

```text
arn:aws:s3:::my-example-bucket
```

Yeh S3 bucket ka ARN hai.

Objects ke liye:

```text
arn:aws:s3:::my-example-bucket/*
```

Yeh us bucket ke objects ko represent karta hai.

### Important Difference

- Bucket-level action: `s3:ListBucket`
- Object-level action: `s3:GetObject`
- Bucket ARN: `arn:aws:s3:::my-example-bucket`
- Object ARN: `arn:aws:s3:::my-example-bucket/*`

Sahi action ke sath sahi resource specify karna bohat zaroori hai.

## 11. What Is Condition?

### Definition
The Condition element specifies circumstances under which a policy statement applies.

### Roman Urdu Explanation
`Condition` ki madad se hum permissions ko additional requirements ke sath restrict kar sakte hain.

Misal ke taur par:
- Specific IP address range se access.
- Specific tag ki condition.
- Specific time ya request attributes, jab supported hon.

### Example: Restrict by Source IP

Neeche sirf example IP range use ki gayi hai. Isay apni approved network range ke mutabiq replace karein.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowListBucketFromApprovedIP",
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::my-example-bucket",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "203.0.113.10/32"
        }
      }
    }
  ]
}
```

Roman Urdu: Yeh example bucket list karne ki permission ko aik specified source IP tak restrict karta hai, agar request context aur doosri applicable policies is access ko allow karti hon.

`203.0.113.10` documentation ke liye reserved example IP hai. Isay real access configuration mein apne approved IP se replace karein.

## 12. What Is Principal?

### Definition
The Principal element identifies the user, role, account, service, or other entity to which a resource-based policy applies.

### Roman Urdu Explanation
`Principal` batata hai ke resource-based policy kis identity ko access dene ya deny karne ke liye apply ho rahi hai.

Yeh element resource-based policies, jaise S3 bucket policies, aur role trust policies mein important hota hai.

Important: Identity-based IAM policies mein aam tor par `Principal` specify nahi kiya jata. In policies ko user, group ya role ke sath attach kiya jata hai.

### Example
S3 bucket policy mein kisi authorized AWS account ya role ko bucket access dene ke liye Principal specify kiya ja sakta hai.

## 13. Identity-Based Policy vs Resource-Based Policy

### Identity-Based Policy

Identity-based policy user, group ya role ke sath attach hoti hai.

Example:
Aik IAM role ko S3 objects read karne ki permission dena.

### Resource-Based Policy

Resource-based policy directly kisi supported resource ke sath attach hoti hai.

Example:
S3 bucket policy ke zariye kisi specified role ko bucket access dena.

### Difference

| Identity-Based Policy | Resource-Based Policy |
|---|---|
| Identity ke sath attach hoti hai | Supported resource ke sath attach hoti hai |
| User, group ya role ko permissions deti hai | Resource tak access define karti hai |
| Identity-based access control ka hissa hai | Resource-based access control ka hissa hai |
| IAM policy evaluation ka aik source hai | IAM policy evaluation ka doosra source ho sakta hai |

Final access decision applicable policies, explicit denies, permission boundaries, organization policies aur doosri relevant controls par depend karta hai.

## 14. Types of IAM Policies

### 1. AWS Managed Policies

AWS ke banaye hue policies jinhein AWS maintain karta hai.

Example: AWS managed read-only policies.

### 2. Customer Managed Policies

Customer apni requirements ke mutabiq policy create aur manage karta hai.

Yeh reusable policies hoti hain jo multiple identities ke sath attach ki ja sakti hain.

### 3. Inline Policies

Inline policy directly aik specific identity ke sath embedded hoti hai.

Inline policies ko carefully manage karna chahiye, kyun ke yeh independent reusable managed policy ki tarah handle nahi hoti.

## 15. What Is Least Privilege?

### Definition
The principle of least privilege means granting only the permissions necessary to perform a required task.

### Roman Urdu Explanation
Least privilege ka matlab hai user ya application ko sirf utna access dena jitna uske kaam ke liye zaroori hai.

Agar kisi user ko files read karni hain, to usay files delete karne ya AWS resources create karne ki permission dena zaroori nahi.

### Example

Incorrect broad access:

```json
{
  "Effect": "Allow",
  "Action": "*",
  "Resource": "*"
}
```

Yeh bohat broad access example hai aur routine use ke liye avoid karna chahiye.

Better approach:
Sirf required actions aur required resources allow karein.

## 16. Practical Example — Read-Only S3 Policy

### Scenario
Aik student ko sirf aik specific S3 bucket ke objects read karne hain.

Student ko objects upload ya delete nahi karne chahiye.

### Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowBucketListing",
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::my-example-bucket"
    },
    {
      "Sid": "AllowObjectReading",
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-example-bucket/*"
    }
  ]
}
```

### Explanation

- `Version` policy language version define karta hai.
- `Statement` permission rules contain karta hai.
- `Effect: Allow` specified actions ko allow karta hai.
- `s3:ListBucket` bucket ke objects list karne deta hai.
- `s3:GetObject` bucket ke objects read karne deta hai.
- `Resource` permission ka scope define karta hai.

Is policy mein `s3:PutObject` aur `s3:DeleteObject` allow nahi kiye gaye.

Important: Is policy ko apply karne se pehle bucket name replace karein aur ensure karein ke identity par koi additional policy unwanted access provide nahi kar rahi.

## 17. Practical Lab — Create a Customer Managed Policy

### Lab Objective
AWS Console mein aik custom IAM policy create karna jo specified S3 bucket ke objects read kar sake.

### Step 1: Open IAM

1. AWS Management Console open karein.
2. IAM service search karein.
3. IAM open karein.
4. Policies select karein.

### Step 2: Create Policy

1. Create policy par click karein.
2. JSON tab select karein.
3. Example read-only S3 policy paste karein.
4. `my-example-bucket` ko apni actual bucket ke naam se replace karein.
5. Policy validate karein.

### Step 3: Name the Policy

Policy ka naam rakhein:

`S3-Specific-Bucket-ReadOnly`

Description:

`Allows listing and reading objects from one specified S3 bucket.`

### Step 4: Review and Create

1. Policy document carefully review karein.
2. Confirm karein ke sirf required actions allow hain.
3. Create policy par click karein.

### Step 5: Attach the Policy

Policy ko suitable test role ya IAM identity ke sath attach karein.

Production user ya role ko policy attach karne se pehle permissions aur business requirement review karein.

### Step 6: Test Permissions

Authorized test identity ke sath required S3 read operation test karein.

Agar permissions sahi hain, to specified bucket ke objects list aur read kiye ja sakte hain, jab koi doosri applicable restriction access ko block na kare.

### Step 7: Verify Denied Actions

Test identity se upload ya delete operation attempt karne ki zaroorat sirf controlled test environment mein hai.

Expected result: Is policy ke zariye upload aur delete ki permission nahi milni chahiye. Lekin doosri policies additional permissions de sakti hain, is liye final access decision verify karein.

## 18. What Is an Explicit Deny?

### Definition
An explicit deny is a policy statement that directly denies a specified action.

### Roman Urdu Explanation
Explicit Deny ka matlab hai kisi action ko clearly block karna.

AWS policy evaluation mein applicable explicit Deny, Allow par precedence rakhta hai.

### Example

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ExplicitlyDenyObjectDeletion",
      "Effect": "Deny",
      "Action": "s3:DeleteObject",
      "Resource": "arn:aws:s3:::my-example-bucket/*"
    }
  ]
}
```

Yeh statement specified bucket ke objects delete karne ke action ko explicitly deny karta hai, jab statement applicable ho.

## 19. What Is a Permission Boundary?

### Definition
A permissions boundary is a policy that sets the maximum permissions an identity-based policy can grant to an IAM user or role.

### Roman Urdu Explanation
Permission boundary aik upper limit ki tarah kaam karti hai. Yeh define karti hai ke identity-based policies ke zariye kisi user ya role ko maximum kitni permissions mil sakti hain.

Sirf permission boundary attach karne se permissions automatically grant nahi hoti. Identity-based policy se required action allow hona bhi zaroori hota hai.

### Example
Aik developer ko S3 read permissions di gayi hain, lekin permission boundary uski possible permissions ko aik defined scope tak limit karti hai.

## 20. What Are Service Control Policies (SCPs)?

### Definition
Service Control Policies are AWS Organizations policies that define the maximum available permissions for accounts or organizational units within an organization.

### Roman Urdu Explanation
SCPs organization-level controls hain jo define kar sakti hain ke organization ke accounts mein maximum kaun si AWS permissions available ho sakti hain.

SCP khud user ko permissions grant nahi karti. Identity-based ya resource-based policies ke zariye required permissions phir bhi honi chahiye.

Note: SCPs AWS Organizations ke context mein use hoti hain aur har standalone AWS account par applicable nahi hoti.

## 21. Common IAM Policy Errors

### Error 1: Incorrect ARN

Agar bucket ya object ARN ghalat ho, to policy expected resource par apply nahi hogi.

Solution:
Bucket ARN aur object ARN verify karein.

### Error 2: Missing Action

Agar required action policy mein included nahi hai, to access denied ho sakta hai.

Solution:
Required action identify karein aur sirf zaroori permission add karein.

### Error 3: Wrong Resource Type

` s3:ListBucket ` bucket-level action hai, jabke ` s3:GetObject ` object-level action hai.

Solution:
Har action ke liye appropriate resource ARN use karein.

### Error 4: Explicit Deny

Koi doosri applicable policy action ko explicitly deny kar sakti hai.

Solution:
Relevant identity policies, resource policies, permission boundaries aur organization policies review karein.

### Error 5: Invalid JSON

Missing comma, incorrect quotation marks ya brackets ki wajah se policy validation fail ho sakti hai.

Solution:
JSON syntax validate karein aur AWS Console ke policy validation messages review karein.

## 22. IAM Policy Security Best Practices

1. Least privilege follow karein.
2. Unnecessary wildcard actions avoid karein.
3. Resource scope ko jitna possible ho restrict karein.
4. Policies ko meaningful names aur descriptions dein.
5. JSON policy ko apply karne se pehle review karein.
6. Production policies ko carefully test karein.
7. Unused policies aur permissions review karein.
8. Explicit Deny ka use samajh kar karein.
9. Access keys aur secrets ko policy files ya public repositories mein expose na karein.
10. CloudTrail aur suitable monitoring tools se AWS activity review karein.
11. Permission boundaries aur organization controls ko samjhein.
12. Policy changes ko document karein.

## 23. Important Interview Questions

### Q1. What is an IAM policy?
An IAM policy is a JSON document that defines permissions for AWS resources and actions.

### Q2. What is the purpose of the Effect element?
It specifies whether a policy statement allows or denies an action.

### Q3. What is the Action element?
It specifies which AWS API operations are allowed or denied.

### Q4. What is the Resource element?
It identifies the AWS resources to which a policy statement applies.

### Q5. What is an ARN?
An Amazon Resource Name identifies an AWS resource.

### Q6. What is a Condition?
A Condition defines circumstances under which a policy statement applies.

### Q7. What is a Principal?
A Principal identifies the entity to which a resource-based policy applies.

### Q8. What is the difference between identity-based and resource-based policies?
Identity-based policies attach to identities, while resource-based policies attach to supported resources.

### Q9. What is explicit deny?
It is a policy statement that directly denies an action. An applicable explicit Deny takes precedence over an Allow.

### Q10. What is least privilege?
It means granting only the permissions required to perform a task.

### Q11. What is a permission boundary?
It sets the maximum permissions that identity-based policies can grant to an IAM user or role.

### Q12. What is an SCP?
An SCP defines maximum available permissions for accounts or organizational units within AWS Organizations.

## 24. Class Summary

- IAM policies AWS resources ke access ko control karti hain.
- IAM policies JSON format mein likhi jati hain.
- `Version` policy language version define karta hai.
- `Statement` permission rules contain karta hai.
- `Effect` Allow ya Deny specify karta hai.
- `Action` AWS operation define karta hai.
- `Resource` target resource identify karta hai.
- `Condition` additional requirements define karti hai.
- `Principal` resource-based policies mein relevant identity identify karta hai.
- ARN AWS resource ko identify karta hai.
- Identity-based aur resource-based policies access control ke different methods hain.
- Explicit Deny applicable Allow par precedence rakhta hai.
- Least privilege permissions ko required scope tak limit karta hai.
- Permission boundaries aur SCPs additional permission limits define kar sakti hain.
- Policy ko apply karne se pehle validate aur test karna zaroori hai.
