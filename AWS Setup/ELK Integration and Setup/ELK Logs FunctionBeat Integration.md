# Functionbeat integration

Now this was a pain, had mutiple errors integrating functionbeat to get logs.

Shout-out to Claude! Helped me fix some of the errors I was getting with log ingestion.

## Issues & Fixes
1. CloudFormation Stack Stuck in ROLLBACK_COMPLETE

Manually deleted stuck stacks with aws cloudformation delete-stack

2. Invalid IAM Permissions
3. Deprecated go1.x Runtime
  - Functionbeat 8.x hardcodes go1.x which AWS deprecated in 2024
Bypassed Functionbeat deploy by manually deploying CloudFormation template with provided.al2 runtime
4. CloudTrail Not Connected to CloudWatch
  - Created IAM role for CloudTrail → CloudWatch
  - Linked trail to log group via aws cloudtrail update-trail\
5. Lambda Connectivity to Elasticsearch
  - Placed Lambda in same VPC and subnet as EC2
  - Updated security group to allow Lambda SG access to port 9200

<img width="1834" height="793" alt="Had to setup nsg for lambda function specifically" src="https://github.com/user-attachments/assets/bdbf2449-cdd9-4495-91a7-017a2a019264" />

**Setup the NSG for ports 9200**

<img width="1915" height="905" alt="Logs now flowing through elk" src="https://github.com/user-attachments/assets/fdb5f8ca-677b-4dfb-b0f6-4bfc95dceb13" />

**Logs now flowing!!**
