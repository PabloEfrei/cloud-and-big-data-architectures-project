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
    
we understand that the authorized actions are to get and to put an object for S3, and to run and terminate an instance for EC2. 
From this snippet : 

    "Resource": [
      "arn:aws:ec2:us-east-1:123456789012:instance/*",
      "arn:aws:s3:::example-bucket/*"
    ]

we understand that the following resources are included (A COMPLETER). 

## Big Data - Data Visualization with AWS Quicksight

