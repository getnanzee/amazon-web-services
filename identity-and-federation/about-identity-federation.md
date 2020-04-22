**Federation in AWS**

- Federation allows users outside of AWS to assume the role for accessing AWS resources
- Federations allows users to login using their thrid party credentials which are trusted by AWS.
- Federation have different types
    - SAML
    - Identity Broker
    - Web Identity Federation with/without Cognito
    - Single Sign On
    - Non-SAML with Microsoft AD
- While using federation, user management is done outside AWS hence we don't need to create IAM users

**SAML Federation**

- It is used to integrate AD/ADFS with AWS
- It allows access to AWS Console and CLI
- No need to create IAM user for each of your employees
- Users sends a request to idP, idP connects with LDAP to fetch the information and sends back the SAML assertion to user, which is then exchanged with STS in AWS to assume the role in AWS
- ADFS supports the similar token exchange
- It uses STS API: AssumeRoleWithSAML

**Custom Identity Broker**

- This is used when the identity store is not SAML compatible
- It uses STS API: AssumeRole or GetFederationToken
- User sends a request to idP, idP connects with indentity store and returns the information to idP, idP then connects to STS to assume the role and return the access to user
- In this case, idP connects with STS and not the user
- Use Custom Identity Broker only if the indentity store is not compatible with SAML

**Web Identity Federation**

- Cognito is the only recommended way to perform Web Identity Federation
- It suports login to anonymous users
- Supports MFA
- Data Sync
- Cognito replaces Token Vending Machine
- Policy variables can be used when using WIF