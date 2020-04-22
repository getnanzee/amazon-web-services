**IAM and all you know**

- Users: long term credentials
- Groups
- Roles: short-term credentials, use STS
    - EC2 Instance Roles: uses EC2 metadata service
    - Service Roles: API Gateway, CodeDeploy etc
    - Cross Account Roles
- Policies
  - AWS Managed
  - Customer Managed
  - Inline Policies
- Resource Based Policy (S3 Bucket, SQS Queue etc)

**IAM Policy Deep Dive**

- Policy Anatomy:
  - json document with
  - Effect
  - Action
  - Resource
  - Condition
  - Policy Variable
- Explicit DENY has precedence over Allow
- Use least privilege for maximum security
    - Access Advisory: Sees permission granted and last used
    - Access Analyzer: Ananlyze resources that are shared with external entities
- Use "NotAction" in AWS policy if you want to DENY all the permission to a resource but explicitly allow few permisison to it.

**IAM Policies Conditions**
```
"Condition" : {"{condition-operator}": {"condition-key","{condition-value}"}}
```

**Operator**
- String (StringEquals, StringNotEquals, StringLike...)
  - "Condition" : {"StringEquals":{"aws:PrincipalTag/job-category":"iamuser-admin"}}
  - "Condition" " {"StringLike" : {"s3:prefix" : ["", "home/", "home/${aws:username}/"]}}
- Numeric (NumericEquals, NumericNotEquals, NumericLessThan...)
- Date (DateEquals, DateNotEquals...)
- Boolean (Bool)
    - "Condition" : {"Bool" :{"aws:SecureTransport" : "True"}}
    - "Condition" : {"Bool" :{"aws:MultiFactorAuthPresent" : "True"}}
- (Not) IpAddress
    - - "Condition" : {"IpAddress" :{"aws:SecureIp" : "345.12.3.1/24"}}

**IAM Policy Variables and Tags**

- Example: ${aws:username}
    - "Resource" : ["arn:aws:s3:::bucketname/${aws:username}/*"]
- AWS Specific:
    - aws:CurrentTime, aws:TokenIssueTime, aws:principaltype, aws:SecureTransport, aws:SourceIp, aws:userid, ec2SourceInstanceARN
- Service Specific:
    - s3:prefix, s3:max-keys, s3:x-amz-acl, sns:Endpoint, sns:Protocol...
- Tag Based:
    - iam:ResourceTag/key-name, aws:PrinicpalTag/key-name