This project demonstrates how to host a static website on Amazon S3 and deliver it globally using Amazon CloudFront with improved performance, security, and HTTPS support.

📌 Project Overview

Host static HTML content on Amazon S3

Serve content globally using CloudFront (CDN)

Enable HTTPS and low-latency access

Beginner-friendly AWS project

🏗 Architecture Diagram
User
  |
  ▼
Amazon CloudFront (CDN)
  |
  ▼
Amazon S3 (Static Website)

🛠 AWS Services Used

Amazon S3 – Static website hosting

Amazon CloudFront – Content Delivery Network

AWS IAM – Access policies

(Optional) Amazon Route 53 – Custom domain

📂 Project Structure
static-website-s3-cloudfront/
│
├── index.html
├── error.html
├── bucket-policy.json
└── README.md

🚀 Deployment Steps
1️⃣ Create Static Website Files
<!DOCTYPE html>
<html>
<head>
  <title>My AWS Static Website</title>
</head>
<body>
  <h1>🚀 Welcome to AWS S3 + CloudFront</h1>
  <p>Static website deployed successfully.</p>
</body>
</html>

2️⃣ Create an S3 Bucket

Bucket name must be globally unique.

aws s3 mb s3://my-static-site-12345

3️⃣ Upload Website Files
aws s3 cp index.html s3://my-static-site-12345/

4️⃣ Enable Static Website Hosting
aws s3 website s3://my-static-site-12345 \
--index-document index.html \
--error-document error.html

5️⃣ Make S3 Bucket Public

Create bucket-policy.json:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-static-site-12345/*"
    }
  ]
}


Apply the policy:

aws s3api put-bucket-policy \
--bucket my-static-site-12345 \
--policy file://bucket-policy.json

6️⃣ Disable Block Public Access
aws s3api put-public-access-block \
--bucket my-static-site-12345 \
--public-access-block-configuration \
BlockPublicAcls=false,IgnorePublicAcls=false,BlockPublicPolicy=false,RestrictPublicBuckets=false

7️⃣ Access Website via S3
http://my-static-site-12345.s3-website-ap-south-1.amazonaws.com

8️⃣ Create CloudFront Distribution (Console)

Go to CloudFront → Create Distribution

Origin Domain → S3 Website Endpoint

Viewer Protocol Policy → Redirect HTTP to HTTPS

Default Root Object → index.html

Create Distribution

⏳ Wait 10–15 minutes for deployment

9️⃣ Access Website via CloudFront
https://<cloudfront-domain-name>

🔐 Security Best Practices (Optional)

Use Origin Access Control (OAC)

Keep S3 bucket private

Allow access only from CloudFront

📈 Benefits of Using CloudFront

Global content delivery

Low latency

HTTPS support

Reduced load on S3

Improved security

🧠 Interview Talking Points

S3 is regional, CloudFront is global

CloudFront caches content at edge locations

HTTPS is not supported directly on S3 website endpoint

CloudFront improves performance and security

📄 Resume Description

Deployed a static website using Amazon S3 and CloudFront, enabling HTTPS, global content delivery, and optimized performance using CDN caching.

🧪 Future Enhancements

Add CI/CD using GitHub Actions

Configure custom domain with Route53

Enable AWS WAF

Add monitoring using CloudWatch

👨‍💻 Author

Mayank Mathur
DevOps Engineer | AWS | CI/CD | Docker
