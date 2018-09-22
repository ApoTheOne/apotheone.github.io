---
title: AWS Lambda, Serverless - Assuming Roles with MFA
date: 2018-09-22 14:33:36
tags: [AWS Lambda, serverless]
categories: [AWS Lambda Serverless]
---

## Setting up AWS Lambda and Serverless with assumed roles and MFA

When IAM User is setup in a way where it assumes a role and along with it if MFA is also enabled then serverless has a problem and has open [issues](https://github.com/serverless/serverless/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+profile+not+found+assume+role+mfa) raised in Github.

---

#### Possible error

`Profile assumedRole not found` with Serverless when using assumed roles and MFA

#### How to reproduce

While deploying a service using serverless using:

`sls deploy -v --aws-profile assumeRole`

#### Error description:

```
Error --------------------------------------------------

Profile XYZ does not exist

For debugging logs, run again after setting the "SLS_DEBUG=*" environment variable.

Get Support --------------------------------------------
Docs: docs.serverless.com
Bugs: github.com/serverless/serverless/issues
Issues: forum.serverless.com
```

---

#### Resolution:

To get temporary credentials using MFA, run:
`aws sts get-session-token --serial-number arn:aws:iam::111111111111:mfa/user.name --token-code 123456`

**Note:**

-   --serial-number is in user IAM's "Security Credentials" section => Assigned MFA device:
    arn:aws:iam::111111111111:mfa/user.name
-   --token-code is the MFA token code.

Output:
{
"Credentials": {
"SecretAccessKey": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
"SessionToken": "tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt",
"Expiration": "2018-09-19T19:53:39Z",
"AccessKeyId": "KKKKKKKKKKKKKKKKKKKKKK"
}
}

Now set AccessKeyId, SecretAccessKey and SessionToken in **mfa** profile's credentials.  
Try deploying the service again using sls deploy command and it should work now.

`sls deploy -v --aws-profile assumeRole`

In order to avoid entering profile parameter again and again you can set environment variable AWS_PROFILE to assumedRole.

-   In Linux bash: `export AWS_Profile="assumedRole"`
-   In Windows CMD: `setx AWS_Profile "assumedRole"`
-   In Windows powershell: `$Env:AWS_Profile = "assumedRole"`

And now just run `sls deploy -v` and it works :satisfied:

Here is the sample of working config and credentials files:

.aws/config file:

```
[default]
region = us-east-1

[profile mfa]
region = us-east-1

[profile assumeRole]
source_profile = mfa
```

.aws/credentials file:

```
[default]
aws_access_key_id = XXXXXXXXXXXXXXXXXXXXXXX
aws_secret_access_key = xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

[mfa]
aws_access_key_id = KKKKKKAccessKeyIdKKKKK
aws_secret_access_key = aaaaaaaaaSecretAccessKeyaaaaaaaaaaaaaa
aws_session_token = ttttttttttttttttttttttttttSessionTokenttttttttttttttttttttttttttttttttttt

[assumeRole]
role_arn = arn:aws:iam::3333333333333:role/RoleName
source_profile = mfa
```

Thank you!
