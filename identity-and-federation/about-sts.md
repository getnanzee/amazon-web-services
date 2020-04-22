**STS to Assume Role**

- Define an IAM Role within your account or cross account
- Define the principle that can access the IAM Role
- Use AWS STS to retrieve credentials and impersonate the IAM Role you have access to (AssumeRole API)
- Temporary credentials validity is between 15 mins to 1 hours

**When to use Role with STS**

- Provide access for an IAM user in one AWS account to access the resources in another account that you own or is owned by third party
- Provide access for services offered by AWS to AWS resources
- Provide access for externally authenticated user (Identity Federation)
- Ability to revoke active sessions and credentials for a role 
    - by adding a policy using a time statement - AWSRevokeOlderSessions
- When you assume a role, you give up your original permisions and take the permissions assigned to the role

**Providing access to AWS account owned by third party**

- Zone of trust = accounts, organizations that you own
- Outside Zone of Trust = 3rd Parties
- Use IAM access analyzer to find out which resources are exposed
- For granting access to 3rd party 
    - AWS Account ID
    - An External Id
        - To uniquely associate the role between you and third party
        - Must be provided when defining the trust and when assuming the role
        - Must be chosen by third party
    - Define permision in IAM policy

**STS Important APIs**

- AssumeRole: access a role within your account or cross account
- AssumeRoleWithSAML: return credentials for users logged with SAML
- AssumeRoleWithWebIdentity: return creds for users loggedwith an idP
    - AWS Cognito, Facebook, Google or any Open-ID Connect compaitble identity provider
    - AWS Cognito is recommended
- GetSessionToken: for MFA, for a user or root user
- GetFederationToken: obtain temporary credentials for federated user
- 
