# AWS\-CreateManagedWindowsInstance<a name="automation-aws-createmanagedwindowsinstance"></a>

**Description**

Create an EC2 instance for a Windows Server that is configured for Systems Manager\.

[Run this Automation \(console\)](https://console.aws.amazon.com/systems-manager/automation/execute/AWS-CreateManagedWindowsInstance)

**Document type**

Automation

**Owner**

Amazon

**Platforms**

Windows

**Parameters**

**Parameters**
+ AmiId

  Type: String

  Default: \{\{ssm:/aws/service/ami\-windows\-latest/Windows\_Server\-2016\-English\-Full\-Base\}\}

  Description: \(Required\) AMI ID to use for launching the instance\.
+ AutomationAssumeRole

  Type: String

  Description: \(Optional\) The Amazon Resource Name \(ARN\) of the AWS Identity and Access Management \(IAM\) role that allows Systems Manager Automation to perform the actions on your behalf\. If no role is specified, Systems Manager Automation uses the permissions of the user that runs this runbook\.
+ GroupName

  Type: String

  Default: SSMSecurityGroupForLinuxInstances

  Description: \(Required\) Security group name to create\.
+ InstanceType

  Type: String

  Default: t2\.medium

  Description: \(Required\) Type of instance to launch\. Default is t2\.medium\.
+ KeyPairName

  Type: String

  Description: \(Required\) Key pair to use when creating instance\.
+ RemoteAccessCidr

  Type: String

  Default: 0\.0\.0\.0/0

  Description: \(Required\) Creates security group with port for RDP \(Port range 3389\) open to IPs specified by CIDR \(default is 0\.0\.0\.0/0\)\. If the security group already exists it will not be modified and rules will not be changed\.
+ RoleName

  Type: String

  Default: SSMManagedInstanceProfileRole

  Description: \(Required\) Role name to create\.
+ StackName

  Type: String

  Default: CreateManagedInstanceStack\{\{automation:EXECUTION\_ID\}\}

  Description: \(Optional\) Specify stack name used by this runbook
+ SubnetId

  Type: String

  Default: Default

  Description: \(Required\) New instance will be deployed into this subnet or in the default subnet if not specified\.
+ VpcId

  Type: String

  Default: Default

  Description: \(Required\) New instance will be deployed into this Amazon Virtual Private Cloud \(Amazon VPC\) or in the default Amazon VPC if not specified\.