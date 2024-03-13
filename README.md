# AWS – Realtime Threat Detection And Prevention
This project (AWS-Real Time Threat Detection and Prevention) is based on implementation of a comprehensive threat monitoring and detection system. In today’s digital landscape, organizations face an ever-increasing number of sophisticated cyber threats. To combat these threats, businesses must implement robust security measures to safeguard their critical assets and data. One such approach is the implementation of a comprehensive threat monitoring and detection system. This project describes how AWS services can be leveraged to build an effective threat monitoring and detection system in Real Time for enhanced security.

GuardDuty is an AWS managed Threat detection service and customers speak a lot about securing their AWS infrastructure and its automated remediation. GuardDuty uses a combination of AWS CloudTrail, Amazon VPC Flow Logs and DNS Logs to detect malicious behaviour and generate alerts if a possible compromise has been detected. A GuardDuty finding represents a potential security issue detected within the network. GuardDuty generates a finding whenever it detects unexpected and potentially malicious activity in your AWS environment. So using GuardDuty, we will deliberately create findings and can see all those events in the GuardDuty console followed by remediation using AWS CloudWatch events and Lambda functions.

PREREQUISITES:

i) GuardDuty
ii) EC2
iii) CloudWatch
iv) IAM
v) AWS Lambda
