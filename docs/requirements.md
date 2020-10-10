## Requirements

This plugin relies on AWS API credentials, using the same configuration files as
the AWS command line.

Such credentials can be configured by the `docker ecs setup` command, either by 
selecting an existing AWS CLI profile from existing config files, or by creating
one passing an AWS access key ID and secret access key.

## Permissions

AWS accounts (or IAM roles) used with the ECS plugin require following permissions:

```yml
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "manually",
            "Effect": "Allow",
            "Action": [
                "ec2:*",
                "ecs:*",
                "logs:*",
                "cloudformation:*",
                "servicediscovery:*",
                "elasticloadbalancing:*",
                "iam:CreateServiceLinkedRole",
                "iam:AttachRolePolicy",
                "iam:CreateRole",
                "iam:PassRole",
                "route53:CreateHostedZone"
            ],
            "Resource": "*"
        }
    ]
}
```

## Okta support

For those relying on [aws-okta](https://github.com/segmentio/aws-okta) to access a managed AWS account 
(as we do at Docker), you can populate your aws config files with temporary access tokens using: 
```shell script
aws-okta write-to-credentials <profile> ~/.aws/credentials
```
