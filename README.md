# AWS – Realtime Threat Detection And Prevention
This project (AWS-Real Time Threat Detection and Prevention) is based on implementation of a comprehensive threat monitoring and detection system. In today’s digital landscape, organizations face an ever-increasing number of sophisticated cyber threats. To combat these threats, businesses must implement robust security measures to safeguard their critical assets and data. One such approach is the implementation of a comprehensive threat monitoring and detection system. This project describes how AWS services can be leveraged to build an effective threat monitoring and detection system in Real Time for enhanced security.

GuardDuty is an AWS managed Threat detection service and customers speak a lot about securing their AWS infrastructure and its automated remediation. GuardDuty uses a combination of AWS CloudTrail, Amazon VPC Flow Logs and DNS Logs to detect malicious behaviour and generate alerts if a possible compromise has been detected. A GuardDuty finding represents a potential security issue detected within the network. GuardDuty generates a finding whenever it detects unexpected and potentially malicious activity in your AWS environment. So using GuardDuty, we will deliberately create findings and can see all those events in the GuardDuty console followed by remediation using AWS CloudWatch events and Lambda functions.

PREREQUISITES:

i) GuardDuty
ii) EC2
iii) CloudWatch
iv) IAM
v) AWS Lambda

**DEMO**
- Created EC2 instance as web server, database server, and compromised machine to demonstrate an attack scenario in network:

![ec2-dashboard](https://github.com/jayramsp/PG-DITISS-Project/assets/146199881/1ece7353-b113-4f2b-8eb6-e208b8769a29) 

- Security group of compromised machine:

  ![security-group-1](https://github.com/jayramsp/PG-DITISS-Project/assets/146199881/2416889a-a03d-4978-834e-7d9c460d93d2)

- created an isolated security group to isolate a compromised machine:

  ![image](https://github.com/jayramsp/PG-DITISS-Project/assets/146199881/9c6965e9-2e2b-4d94-a1cd-538b3dae8631)

- Created CloudWatch rules for SNS and AWS Lambda function:
  
  ![cloudwatch-rules](https://github.com/jayramsp/PG-DITISS-Project/assets/146199881/af038af6-78b7-498d-b59f-ecb4aa416630)

- Configured SNS for desired endpoint mail ID:

  ![sns-endpoint](https://github.com/jayramsp/PG-DITISS-Project/assets/146199881/c65e114a-5afc-4f66-ac43-38f7d77990b2)

- Configured GuardDuty to scan malicious activities:

  ![guardduty-finding](https://github.com/jayramsp/PG-DITISS-Project/assets/146199881/0a506a6f-802a-4821-85f1-9eb4c88af515)

- Lambda function code to isolate an compromised instance by changing security group:

  ![lambda-function](https://github.com/jayramsp/PG-DITISS-Project/assets/146199881/c61bff8a-fba8-47d0-921c-295b8da248ad)

- Performing nmap to demonstrate portscan attack:

  ![nmap-1](https://github.com/jayramsp/PG-DITISS-Project/assets/146199881/a02b5a38-5f89-4d16-ad4a-c2f0b2ea1c2c)

- CloudWatch logs after Attack is detected:

  ![cloudwatch-logs (1)](https://github.com/jayramsp/PG-DITISS-Project/assets/146199881/25b2ee05-af3a-4a8d-b12b-0a836ad8a3b8)

- SNS mail alert with JSON file:

  ![sns-alert](https://github.com/jayramsp/PG-DITISS-Project/assets/146199881/17c92faa-7407-4280-a5e8-f4d56197efca)

- After Attack is detected the security group of Compromised instance from attacker is performing portscan is changed to isolated group:

  ![security-group-1 (1)](https://github.com/jayramsp/PG-DITISS-Project/assets/146199881/5cd9b95f-e017-4bdd-98cb-f0eef037cd14)

- The SSH connection gets automatically disconnected in real time:

  ![nmap-2](https://github.com/jayramsp/PG-DITISS-Project/assets/146199881/6e87f8eb-b119-4aec-9572-aa2b2d318083)

All these network activities are stored in VPC flow logs which GuardDuty takes as input for threat analysis. Now doing port scanning and pinging to malicious host from compromised instance that will give us Recon:EC2/Portscan and unauthorized EC2 access malicious IP caller finding on the GuardDuty console. Now it takes a few minutes to display the finding on the GuardDuty console. Findings are automatically sent to CloudWatch Events and new findings are exported within 5 minutes.

After the required amount of time, the CloudWatch event rule will receive those finding logs and if the finding events are matched it will invoke target service. Here we have SNS Topic and Lambda function as out target service. SNS Topic subscribers will receive an email notification containing finding details.

Now when Lambda gets triggered it will change the security group of the compromised instance. Compromised instances details are available in the event logs and the Lambda function is extracting the affected instance details from the event variable. The Security Group will isolate the compromised instance from the whole infrastructure.

In this way we can identify threats using GuardDuty on our AWS infrastructure and have an automated prevention mechanism using AWS Lambda functions.


