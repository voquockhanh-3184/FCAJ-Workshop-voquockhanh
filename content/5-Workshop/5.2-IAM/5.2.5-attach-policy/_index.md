---
title : "Attach IAM Permission Policy"
date : 2024-01-01 
weight : 5
chapter : false
pre : " <b> 5.2.5. </b> "
---

Attach IAM permission policy to configure appropriate permissions for deploying and cleaning up resources throughout the Examora workshop.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ExamoraCoreServerlessServices",
      "Effect": "Allow",
      "Action": [
        "cognito-idp:*",
        "ses:*",
        "secretsmanager:*",
        "lambda:*",
        "apigateway:*",
        "execute-api:*",
        "s3:*",
        "sqs:*",
        "logs:*",
        "cloudwatch:*",
        "xray:*",
        "amplify:*",
        "route53:*",
        "acm:ListCertificates",
        "acm:DescribeCertificate",
        "acm:RequestCertificate",
        "acm:DeleteCertificate",
        "acm:AddTagsToCertificate",
        "acm:ListTagsForCertificate",
        "sts:GetCallerIdentity",
        "tag:GetResources",
        "tag:TagResources",
        "tag:UntagResources"
      ],
      "Resource": "*"
    },
    {
      "Sid": "ExamoraCloudFormationForSamLite",
      "Effect": "Allow",
      "Action": [
        "cloudformation:CreateStack",
        "cloudformation:UpdateStack",
        "cloudformation:DeleteStack",
        "cloudformation:DescribeStacks",
        "cloudformation:DescribeStackEvents",
        "cloudformation:DescribeStackResources",
        "cloudformation:GetTemplate",
        "cloudformation:ValidateTemplate",
        "cloudformation:CreateChangeSet",
        "cloudformation:DescribeChangeSet",
        "cloudformation:ExecuteChangeSet",
        "cloudformation:DeleteChangeSet",
        "cloudformation:ListStacks",
        "cloudformation:ListStackResources",
        "cloudformation:GetTemplateSummary"
      ],
      "Resource": "*"
    },
    {
      "Sid": "ExamoraIAMRoleAndPolicyManagement",
      "Effect": "Allow",
      "Action": [
        "iam:CreateRole",
        "iam:DeleteRole",
        "iam:GetRole",
        "iam:UpdateRole",
        "iam:TagRole",
        "iam:UntagRole",
        "iam:PassRole",
        "iam:AttachRolePolicy",
        "iam:DetachRolePolicy",
        "iam:PutRolePolicy",
        "iam:DeleteRolePolicy",
        "iam:GetRolePolicy",
        "iam:ListRolePolicies",
        "iam:ListAttachedRolePolicies",
        "iam:CreatePolicy",
        "iam:DeletePolicy",
        "iam:GetPolicy",
        "iam:GetPolicyVersion",
        "iam:ListPolicyVersions",
        "iam:CreatePolicyVersion",
        "iam:DeletePolicyVersion",
        "iam:SetDefaultPolicyVersion",
        "iam:ListPolicies",
        "iam:ListRoles"
      ],
      "Resource": "*"
    },
    {
      "Sid": "AllowReadAWSManagedPolicies",
      "Effect": "Allow",
      "Action": [
        "iam:GetPolicy",
        "iam:GetPolicyVersion",
        "iam:ListPolicies"
      ],
      "Resource": "*"
    }
  ]
}
```
