# Cloud and Big Data Architecture - Final Project 

## Group

Guillaume Théret - Pablo Sanchez - M1 SE2

## Task 1 (App deployment)


## Quizz

### IAM quizz 

#### Question 1 

![IAM1](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/iam%20quizz/1.png)

#### Answer : Option 3

#### Question 2

![IAM2](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/iam%20quizz/2.png)

#### Answer : Option 1

#### Question 3

![IAM3](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/iam%20quizz/3.png)

#### Answer : Options 3 and 4

#### Question 4

![IAM4](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/iam%20quizz/4.png)

#### Answer : Option 4

#### Question 5

![IAM5](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/iam%20quizz/5.png)

#### Answer : Option 2

#### Question 6

![IAM6](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/iam%20quizz/6.png)

#### Answer : Option 3

#### Question 7

![IAM7](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/iam%20quizz/7.png)

#### Answer : Option 1


#### Network quizz 

#### Question 1

![NETWORK1](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/network%20quizz/1.png)

#### Answer : Option 3

#### Question 2

![NETWORK2](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/network%20quizz/2.png)

#### Answer : Option 3

#### Question 3

![NETWORK3](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/network%20quizz/3.png)

#### Answer : Options 3, 5 and 6

#### Question 4

![NETWORK4](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/network%20quizz/4.png)

#### Answer : Option 4

## IAM

### Policies evaluation

#### Questions : What actions are allowed for EC2 instances and S3 objects based on this policy? What specific resources are included?

    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "AllowEC2AndS3",
          "Effect": "Allow",
          "Action": [
            "ec2:RunInstances",
            "ec2:TerminateInstances",
            "s3:GetObject",
            "s3:PutObject"
          ],
          "Resource": [
            "arn:aws:ec2:us-east-1:123456789012:instance/*",
            "arn:aws:s3:::example-bucket/*"
          ]
        }
      ]
    }

#### Answers : 

From this snippet : 

    "Action": [
      "ec2:RunInstances",
      "ec2:TerminateInstances",
      "s3:GetObject",
      "s3:PutObject"
    ]
    
we understand that the authorized actions are to get and to put an object for S3 (read and add an object), and to run and terminate an instance for EC2 (create and terminate an instance). 

From this snippet : 

    "Resource": [
      "arn:aws:ec2:us-east-1:123456789012:instance/*",
      "arn:aws:s3:::example-bucket/*"
    ]

we understand that the following resources are included (A COMPLETER). 

#### Questions : Under what condition does this policy allow access to VPC-related information? Which AWS region is specified?

    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "AllowVPCAccess",
          "Effect": "Allow",
          "Action": [
            "ec2:DescribeVpcs",
            "ec2:DescribeSubnets",
            "ec2:DescribeSecurityGroups"
          ],
          "Resource": "*",
          "Condition": {
            "StringEquals": {
              "aws:RequestedRegion": "us-west-2"
            }
          }
        }
      ]
    }

#### Answers : 

From this snippet : 

(A COMPLETER)

From this snippet : 

    "aws:RequestedRegion": "us-west-2"

we understand that AWS region is the US West (Oregon) region. 

#### Questions : What actions are allowed on the "example-bucket" and its objects based on this policy? What specific prefixes are specified in the condition?

    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "AllowIAMUserCreation",
          "Effect": "Allow",
          "Action": "iam:CreateUser",
          "Resource": "arn:aws:iam::123456789012:user/${aws:username}"
        },
        {
          "Sid": "AllowIAMUserDeletion",
          "Effect": "Allow",
          "Action": "iam:DeleteUser",
          "Resource": "arn:aws:iam::123456789012:user/${aws:username}"
        }
      ]
    }

#### Answers : 

From this snippet : 

    "Action": ["s3:GetObject", "s3:PutObject", "s3:ListBucket"],

we understand that the "example-bucket" allows to get and put objects in order to read (get) or add an object, as well as returning a list of buckets owned by the request sender. 

From this snippet : 

    "s3:prefix": ["documents/*", "images/*"]

we understand that that the prefixes are documents/* and images/*, meaning that the object are stocked in folders documents and images.

#### Questions : What actions are allowed for IAM users based on this policy? How are the resource ARNs constructed?

    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "AllowIAMUserCreation",
          "Effect": "Allow",
          "Action": "iam:CreateUser",
          "Resource": "arn:aws:iam::123456789012:user/${aws:username}"
        },
        {
          "Sid": "AllowIAMUserDeletion",
          "Effect": "Allow",
          "Action": "iam:DeleteUser",
          "Resource": "arn:aws:iam::123456789012:user/${aws:username}"
        }
      ]
    }

#### Answers : 

From this snippet : 

    {
      "Sid": "AllowIAMUserCreation",
      "Effect": "Allow",
      "Action": "iam:CreateUser",
      ...
    },
    {
      "Sid": "AllowIAMUserDeletion",
      "Effect": "Allow",
      "Action": "iam:DeleteUser",
      ...
    }
    
we understand that it is possible to create and delete IAM users.

From these two lines : 

    {
      ...
      "Resource": "arn:aws:iam::123456789012:user/${aws:username}"
    },
    {
      ...
      "Resource": "arn:aws:iam::123456789012:user/${aws:username}"
    }
    
we understand that the resources ARNs are constructed by IAM unique automatically generated number (here 123456789012) and manually defined user name (${aws:username}).

#### Questions : 
- Which AWS service does this policy grant you access to ?
- Does it allow you to create an IAM user, group, policy, or role ?
- Go to https://docs.aws.amazon.com/IAM/latest/UserGuide/ and in the left navigation expand Reference > Policy Reference > Actions, Resources, and Condition Keys. Choose Identity And Access Management. Scroll to the Actions Defined by Identity And Access Management list. Name at least three specific actions that the iam:Get* action allows.

        {
          "Version": "2012-10-17",
          "Statement": {
            "Effect": "Allow",
            "Action": ["iam:Get*", "iam:List*"],
            "Resource": "*"
          }
        }

#### Answers : 

This policy grant access to IAM AWS service.

The given code doesn't allow to create a IAM user, group, policy, or role. The actions Get* and List* allow the user to use any specific action starting by "Get" or "List", but there are onyl reading actions. 

The snippet : 

    ["iam:Get*",

allows the users to use the following specific actions : GetAccountName, GetGroupPolicy, or GetLoginProfile (or any other action starting by "Get").

#### Questions : 
- What actions does the policy allow?
- Say that the policy included an additional statement object, like this example :

        {
          "Effect": "Allow",
          "Action": "ec2:*"
        }

- How would the policy restrict the access granted to you by this additional statement ?
- If the policy included both the statement on the left and the statement in question 2, could you terminate an m3.xlarge instance that existed in the account ?

        {
          "Version": "2012-10-17",
          "Statement": [
            {
              "Condition": {
                "StringEquals": {
                  "ec2:InstanceType": ["t2.micro", "t2.small"]
                }
              },
              "Resource": "arn:aws:ec2:*:*:instance/*",
              "Action": ["ec2:RunInstances", "ec2:StartInstances"],
              "Effect": "Deny"
            }
          ]
        }

#### Answers : 

From this snippet : 

    "Action": ["ec2:RunInstances", "ec2:StartInstances"],

we understand that this policy allows the user to run an EC2 instance (create + start), and start an already existing but stopped EC2 instance.

(A COMPLETER)
(A COMPLETER)

## Big Data - Data Visualization with AWS Quicksight
