# Deploy Instance
## Create Key Pair

* [AWS CLI - Create Key Pair](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-key-pair.html)

```
aws ec2 create-key-pair ^
    --key-name KEY-I346-SUB-DEVOPSTEAM01 ^
    --key-type rsa ^
    --key-format pem ^
    --region eu-central-1 ^
    --profile devopsteam01 ^
    --output text > KEY-I346-SUB-DEVOPSTEAM01.pem
```

OUTPUT
```
a file "<name>.pem" has been created
```

## Create security group

* [AWS CLI - Create security group]([https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-subnet.html](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-security-group.html?highlight=security%20group))


```
aws ec2 create-security-group ^
 --group-name secugrp-i346-devopsteam01 ^
 --description "secugrp-i346-devopsteam01" ^
 --vpc-id vpc-0a22d771f16ae549d
```
OUTPUT
```
{
    "GroupId": "sg-054321d87f9af9ac3",
    "SecurityGroupArn": "arn:aws:ec2:eu-central-1:709024702237:security-group/sg-054321d87f9af9ac3"
}

```


## Authorize Security Group - Ingress

* [AWS CLI - Authorize Security Group - Ingress](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/authorize-security-group-ingress.html)

```
aws ec2 authorize-security-group-ingress^
 --group-id sg-054321d87f9af9ac3^
 --ip-permissions "IpProtocol=tcp,FromPort=22,ToPort=22,IpRanges=[{CidrIp=10.0.0.0/28,Description=SSH-FROM-DMZ}]"^
 --region eu-central-1 ^
--profile devopsteam01 ^
--output table
```

OUTPUT
```
---------------------------------------------------------------------------------------------------------------
|                                        AuthorizeSecurityGroupIngress                                        |
+------------------------------------------------------------+------------------------------------------------+
|  Return                                                    |  True                                          |
+------------------------------------------------------------+------------------------------------------------+
||                                            SecurityGroupRules                                             ||
|+----------------------+------------------------------------------------------------------------------------+|
||  CidrIpv4            |  10.0.0.0/28                                                                       ||
||  Description         |  SSH-FROM-DMZ                                                                      ||
||  FromPort            |  22                                                                                ||
||  GroupId             |  sg-054321d87f9af9ac3                                                              ||
||  GroupOwnerId        |  709024702237                                                                      ||
||  IpProtocol          |  tcp                                                                               ||
||  IsEgress            |  False                                                                             ||
||  SecurityGroupRuleArn|  arn:aws:ec2:eu-central-1:709024702237:security-group-rule/sgr-012088607fe340ee2   ||
||  SecurityGroupRuleId |  sgr-012088607fe340ee2                                                             ||
||  ToPort              |  22                                                                                ||
|+----------------------+------------------------------------------------------------------------------------+|
```
## Run Instance

* [AWS CLI - Run instance](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/run-instances.html)
```
aws ec2 run-instances ^
--image-id ami-0584590e5f0e97daa ^
 --instance-type t2.micro ^
--key-name KEY-I346-SUB-DEVOPSTEAM01 ^
 --subnet-id subnet-0fc3126df64eea2b9 ^
 --security-group-ids sg-054321d87f9af9ac3 ^
 --tag-specifications ResourceType=instance,Tags=[{Key=Name,Value=EC2-DEVOPSTEAM01-SUBNET}] ^
 --private-ip-address 10.0.01.11 ^
 --region eu-central-1 ^
--profile devopsteam01 ^
 --output table
```

OUTPUT
```
nous avons perdu le tableau pour le run instance
```

## Rule RDP instance
```
aws ec2 authorize-security-group-ingress \
    --group-id sg-054321d87f9af9ac3 \
    --ip-permissions "IpProtocol=tcp,FromPort=3389,ToPort=3389,IpRanges=[{CidrIp=10.0.0.0/28,Description=RDP-FROM-DMZ}]" \
    --region eu-central-1 \
    --profile devopsteam01 \
    --output table
```
OUTPUT
```
---------------------------------------------------------------------------------------------------------------
|                                        AuthorizeSecurityGroupIngress                                        |
+------------------------------------------------------------+------------------------------------------------+
|  Return                                                    |  True                                          |
+------------------------------------------------------------+------------------------------------------------+
||                                            SecurityGroupRules                                             ||
|+----------------------+------------------------------------------------------------------------------------+|
||  CidrIpv4            |  10.0.0.0/28                                                                       ||
||  Description         |  RDP-FROM-DMZ                                                                      ||
||  FromPort            |  3389                                                                              ||
||  GroupId             |  sg-054321d87f9af9ac3                                                              ||
||  GroupOwnerId        |  709024702237                                                                      ||
||  IpProtocol          |  tcp                                                                               ||
||  IsEgress            |  False                                                                             ||
||  SecurityGroupRuleArn|  arn:aws:ec2:eu-central-1:709024702237:security-group-rule/sgr-09e88cea6ab3528c5   ||
||  SecurityGroupRuleId |  sgr-09e88cea6ab3528c5                                                             ||
||  ToPort              |  3389                                                                              ||
|+----------------------+------------------------------------------------------------------------------------+|

```

