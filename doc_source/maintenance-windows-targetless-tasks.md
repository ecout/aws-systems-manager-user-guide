# Registering maintenance window tasks without targets<a name="maintenance-windows-targetless-tasks"></a>

**Note**  
The ability to register tasks without targets is not currently supported in the AWS Systems Manager console\.

For each maintenance window you create, you can specify one or more tasks to perform when the maintenance window runs\. In most cases, you must specify the resources, or targets, that the task is to run on\. In some cases, however, you do not need to specify targets explicitly in the task\.

One or more targets must be specified for maintenance window Systems Manager Run Command\-type tasks\. Depending on the nature of the task, targets are optional for other maintenance window task types \(Systems Manager Automation, AWS Lambda, and AWS Step Functions\)\. 

For Lambda and Step Functions task types, whether a target is required depends on the content of the function or state machine you have created\.

Automation tasks more commonly don't need a target specified explicitly for a task\. For example, say that you are creating an Automation\-type task to update an Amazon Machine Image \(AMI\) for Linux using the `AWS-UpdateLinuxAmi` runbook\. When the task runs, the AMI is updated with the latest available Linux distribution packages and Amazon software\. New instances created from the AMI already have these updates installed\. Because the ID of the AMI to be updated is specified in the input parameters for the runbook, there is no need to specify a target again in the maintenance window task\.

Similarly, suppose you are using the AWS Command Line Interface \(AWS CLI\) to register a maintenance window Automation task that uses the document [AWS\-RestartEC2Instance](automation-aws-restartec2instance.md)\. Because the instance to restart is specified in the `--task-invocation-parameters` argument, you don't need to also specify a `--targets` option\. 

**Note**  
For maintenance window tasks without a target specified, you cannot supply values for `--max-errors` and `--max-concurrency`\. Instead, the system inserts a placeholder value of `1`, which may be reported in the response to commands such as [describe\-maintenance\-window\-tasks](https://docs.aws.amazon.com/cli/latest/reference/ssm/describe-maintenance-window-tasks.html) and [get\-maintenance\-window\-task](https://docs.aws.amazon.com/cli/latest/reference/ssm/get-maintenance-window-task.html)\. These values do not affect the running of your task and can be ignored\.

The following example demonstrates omitting the `--targets`,`--max-errors`, and `--max-concurrency` options for a targetless maintenance window task\.

------
#### [ Linux & macOS ]

```
aws ssm register-task-with-maintenance-window \
    --window-id "mw-ab12cd34eEXAMPLE" \
    --service-role-arn "arn:aws:iam::123456789012:role/MaintenanceWindowAndAutomationRole" \
    --task-type "AUTOMATION" \
    --name "RestartInstanceWithoutTarget" \
    --task-arn "AWS-RestartEC2Instance" \
    --task-invocation-parameters "{\"Automation\":{\"Parameters\":{\"InstanceId\":[\"i-02573cafcfEXAMPLE\"]}}}" \
    --priority 10
```

------
#### [ Windows ]

```
aws ssm register-task-with-maintenance-window ^
    --window-id "mw-ab12cd34eEXAMPLE" ^
    --service-role-arn "arn:aws:iam::123456789012:role/MaintenanceWindowAndAutomationRole" ^
    --task-type "AUTOMATION" ^
    --name "RestartInstanceWithoutTarget" ^
    --task-arn "AWS-RestartEC2Instance" ^
    --task-invocation-parameters "{\"Automation\":{\"Parameters\":{\"InstanceId\":[\"i-02573cafcfEXAMPLE\"]}}}" ^
    --priority 10
```

------

**Note**  
For maintenance window tasks registered before December 23, 2020: If you specified targets for the task and one is no longer required, you can update that task to remove the targets using the Systems Manager console or the [update\-maintenance\-window\-task](https://docs.aws.amazon.com/cli/latest/reference/ssm/update-maintenance-window-task.html) AWS CLI command\.

**Related content**

[Error messages: "Maintenance window tasks without targets do not support MaxConcurrency values" and "Maintenance window tasks without targets do not support MaxErrors values"](troubleshooting-maintenance-windows.md#maxconcurrency-maxerrors-not-supported)