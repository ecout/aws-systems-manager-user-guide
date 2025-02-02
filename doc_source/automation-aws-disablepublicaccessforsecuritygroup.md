# AWS\-DisablePublicAccessForSecurityGroup<a name="automation-aws-disablepublicaccessforsecuritygroup"></a>

 **Description** 

This runbook disables default SSH and RDP ports that are opened to all IP addresses\.

**Important**  
This runbook fails with an "InvalidPermission\.NotFound" error for security groups that meet both of the following criteria: 1\) The security group is located in a non\-default VPC; and 2\) The inbound rules for the security group don't specify open ports using all four of the following patterns:   
`0.0.0.0/0`
`::/0`
`SSH or RDP port + 0.0.0.0/0`
`SSH or RDP port + ::/0`

**Note**  
This runbook is not available in the AWS Regions located within China\.

[Run this Automation \(console\)](https://console.aws.amazon.com/systems-manager/automation/execute/AWS-DisablePublicAccessForSecurityGroup)

**Document type**

Automation

**Owner**

Amazon

**Platforms**

Linux, macOS, Windows

**Parameters**
+ AutomationAssumeRole

  Type: String

  Description: \(Optional\) The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role that allows Systems Manager Automation to perform the actions on your behalf\. If no role is specified, Systems Manager Automation uses the permissions of the user that runs this runbook\.
+ GroupId

  Type: String

  Description: \(Required\) The ID of the security group for which the ports should be disabled\.
+ IpAddressToBlock

  Type: String

  Description: \(Optional\) Additional IPv4 addresses from which access should be blocked, in the format `1.2.3.4/32`\.

 **Outputs** 

None