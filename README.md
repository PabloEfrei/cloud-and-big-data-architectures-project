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

#### Question : What actions are allowed for EC2 instances and S3 objects based on this policy? What specific resources are included?

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

#### Answer : 

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

#### Question : Under what condition does this policy allow access to VPC-related information? Which AWS region is specified?

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

#### Answer : 

From this snippet : 

(A COMPLETER)

From this snippet : 

    "aws:RequestedRegion": "us-west-2"

we understand that AWS region is the US West (Oregon) region. 

#### Question : What actions are allowed on the "example-bucket" and its objects based on this policy? What specific prefixes are specified in the condition?

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

#### Answer : 

From this snippet : 

    "Action": ["s3:GetObject", "s3:PutObject", "s3:ListBucket"],

we understand that the "example-bucket" allows to get and put objects in order to read (get) or add an object, as well as returning a list of buckets owned by the request sender. 

From this snippet : 

    "s3:prefix": ["documents/*", "images/*"]

we understand that AWS region is the US West (Oregon) region. 


## Big Data - Data Visualization with AWS Quicksight

