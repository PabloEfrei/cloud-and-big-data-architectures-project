# Cloud and Big Data Architecture - Final Project 

## Group

Guillaume Théret - Pablo Sanchez - M1 SE2

___
## Task 1 - App deployment

### Solution Requirements 

#### Architecture diagram for Infrastructure solution 

![diagram](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/diagram.jpg)

In this diagram:

- The VPC contains both a public subnet and a private subnet.
- The EC2 instance is placed in the public subnet to allow public access to the website.
- The RDS (MySQL) database instance is placed in the private subnet to prevent public access and enhance security.
- The Internet Gateway allows communication between the VPC and the Internet.

####  Our own defined network infrastructure

Create a VPC :

![vpc](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/Step1_vpc.jpg)

Create 4 subnets (private,public, area A, area B) :

![subnet](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/Step2_subnet.jpg)

Create internet gateway :

![ig](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/Step3_internetgateway.jpg)

Create route :

![table route](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/Step4_tableroute.jpg)

Create security group (relevant for EC2 instance) :

![secgroup](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/Step5_securitygroup.jpg)

Link public subnet to route :

![assoc](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/Step6_associationsubnetandroute.jpg)

#### Secure Hosting of MySQL database - private only

![db](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/Step1_db.jpg)

#### EC2 Instance Connect to connect to the database from local machine

Create Instance : 
![instance](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/createinstance.jpg)

####  Use of specified endpoints

![param](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/parametres.jpg)
![param1](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/parametres_db.jpg)
![param2](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/parametres_endpoint.jpg)
![param3](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/parametres_password.jpg)
![param4](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/project_screenshots/parametres_username.jpg)

___
## Task 2 - Quizz

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

___
## Task 3 - IAM

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

we understand that the policy gives access to all EC2 instances from account 123456789012 in region us-east-1, and in S3 "example-bucket".

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

    "Condition": {
            "StringEquals": {
              "aws:RequestedRegion": "us-west-2"
            }

we understand that AWS region is the US West (Oregon) region, and that this policy allows access to VPC-related information only for requests in the us-west-2 region. 

#### Questions : Under what condition does this policy allow access to VPC-related information? Which AWS region is specified?

    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "AllowS3ReadWrite",
          "Effect": "Allow",
          "Action": ["s3:GetObject", "s3:PutObject", "s3:ListBucket"],
          "Resource": [
            "arn:aws:s3:::example-bucket",
            "arn:aws:s3:::example-bucket/*"
          ],
          "Condition": {
            "StringLike": {
              "s3:prefix": ["documents/*", "images/*"]
            }
          }
        }
      ]
    }

#### Answers : 

From this snippet : 

    "Action": ["s3:GetObject", "s3:PutObject", "s3:ListBucket"],

we understand that the "example-bucket" allows to get and put objects in order to read (get) or add an object, as well as returning a list of buckets owned by the request sender. 

From this snippet : 

    "s3:prefix": ["documents/*", "images/*"]

we understand that the 3 given S3 actions are restricted to folders with prefixes documents/* and images/* from S3 bucket example-bucket .

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
    
we understand that the resources ARNs are constructed with AWS account ID (here 123456789012) and with manually defined user name (${aws:username}).

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

The given code doesn't allow to create a IAM user, group, policy, or role. The actions Get* and List* allow the user to use any specific action starting by "Get" or "List", but they are only reading actions. 

The snippet : 

    ["iam:Get*",

allows grant access to the following specific actions : GetAccountName, GetGroupPolicy, or GetLoginProfile (or any other action starting by "Get").

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

we understand that this policy allows users to run and start EC2 instances of the specified instance types t2.micro and t2.small.

When this is added : 

    {
      "Effect": "Allow",
      "Action": "ec2:*"
    }

the goal is to grants unrestricted access to perform any EC2-related action. But the "Effect" : "Deny" is more restrictive than the "Effect" : "Allow", thus the additional statement allowing all "ec2:*" actions would be overridden by the first statement. Hence the policy would still restrict the actions to only "ec2:RunInstances" and "ec2:StartInstances" on the specified instance types, and all other EC2 actions would be denied.

It is not possible to determine the specific actions allowed or denied for the "m3.xlarge" instance type, because the "ec2:*" action is allowed, implying unrestricted access to perform any EC2-related action. 

But the first statement in the original policy denies the "ec2:RunInstances" and "ec2:StartInstances" actions for the "t2.micro" and "t2.small" instance types.
The policy does not explicitly mention the "m3.xlarge" instance type or the "ec2:TerminateInstances" action, we cannot determine whether terminating an "m3.xlarge" instance is allowed or denied.

Therefore the policy would need to include a statement that either allows or denies the "ec2:TerminateInstances" action and specifies the appropriate conditions or resources. Without such information, it is not possible to determine if terminating an "m3.xlarge" instance is allowed or not.

___
## Task 4 - Big Data - Data Visualization with AWS Quicksight

### Complete Dashboard

[Click here][dashboardPDF] to see pdf version.

![totaldashboard](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/quicksight/total_dashboard.jpg)

### How to build the Sum of Revenue by Admit Date

![quicksight1](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/quicksight/build_sum_of_revenue_by_admit_date.jpg)

### How to build the Sum of Profit by Hospital

![quicksight2](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/quicksight/build_sum_of_profit_by_hospital.jpg)

### How to build the YoY Revenue (2018 vs 2017)

![quicksight3](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/quicksight/build_yoy_revenue.jpg)

### How to build the YoY Profit (2018 vs 2017)

![quicksight4](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/quicksight/build_yoy_profit.jpg)

### How to build the Sum of Cost by Category and Admit Date

![quicksight5](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/quicksight/build_sum_of_cost_by_category_and_admit_date.jpg)

### How to build the Sum of Discount and Sum of Profit by Admin Date and Category 

![quicksight6](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/quicksight/build_sum_of_discoun_and_sum_of_profit_by_admit_date_and_category.jpg)

### How to build the Period over period

![quicksight7](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/quicksight/build_period_over_period.jpg)

### How to build the Top 3 Category

![quicksight8](https://github.com/PabloEfrei/cloud-and-big-data-architectures-project/blob/main/assets/quicksight/build_top_3_categories.jpg)


[dashboardPDF]: <assets/quicksight/dashboard.pdf>
