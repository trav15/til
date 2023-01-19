# CLI

The `describe-instances` command describes the specified instances or all instances. Optionally, you can add parameters to the describe-instances to modify its function.

Here is the list of the available parameters for describe-instances:
```
[–dry-run | –no-dry-run] 
[–instance-ids ] 
[–filters ]
[–cli-input-json ] 
[–starting-token ] 
[–page-size ] 
[–max-items ] 
[–generate-cli-skeleton]
```
The `–dry-run` parameter checks whether you have the required permissions for the action, without actually making the request, and provides an error response. If you have the required permissions, the error response is DryRun-Operation. Otherwise, it is UnauthorizedOperation.

## *Resources*
- [AWS docs CLI help](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-help.html)
- [AWS docs describe-instances](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-instances.html)