## Deploy Instance

## Create security group

* [AWS CLI - Create security group]([https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-subnet.html](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-security-group.html?highlight=security%20group))


```
aws ec2 create-security-group ^
 --group-name secugrp-i346-devopsteam01 ^
 --description "secugrp-i346-devopsteam01" ^
 --vpc-id vpc-0a22d771f16ae549d
```

```
{
    "GroupId": "sg-054321d87f9af9ac3",
    "SecurityGroupArn": "arn:aws:ec2:eu-central-1:709024702237:security-group/sg-054321d87f9af9ac3"
}
