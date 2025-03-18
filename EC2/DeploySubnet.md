# DeploySubnet


## Find VPC id

* [AWS CLI - Describe VPCs](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/describe-vpcs.html)

```
aws ec2 describe-vpcs ^
    --region eu-central-1 ^ 
    --profile devopsteam01 ^
    --output table
```

OUTPUT
```
-----------------------------------------------------------
|                      DescribeVpcs                       |
+---------------------------------------------------------+
||                         Vpcs                          ||
|+----------------------+--------------------------------+|
||  CidrBlock           |  10.0.0.0/16                   ||
||  DhcpOptionsId       |  dopt-05854b009a610ac91        ||
||  InstanceTenancy     |  default                       ||
||  IsDefault           |  False                         ||
||  OwnerId             |  709024702237                  ||
||  State               |  available                     ||
||  VpcId               |  vpc-0a22d771f16ae549d         ||
|+----------------------+--------------------------------+|
|||               BlockPublicAccessStates               |||
||+------------------------------------------+----------+||
|||  InternetGatewayBlockMode                |  off     |||
||+------------------------------------------+----------+||
|||               CidrBlockAssociationSet               |||
||+----------------+------------------------------------+||
|||  AssociationId |  vpc-cidr-assoc-0fad6e9a11ccae331  |||
|||  CidrBlock     |  10.0.0.0/16                       |||
||+----------------+------------------------------------+||
||||                  CidrBlockState                   ||||
|||+-------------------+-------------------------------+|||
||||  State            |  associated                   ||||
|||+-------------------+-------------------------------+|||
|||                        Tags                         |||
||+----------------------+------------------------------+||
|||  Key                 |  Name                        |||
|||  Value               |  vpc-i346                    |||
||+----------------------+------------------------------+||
```

## Get a list of existing subnets

* [AWS CLI - List subnets](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/describe-subnets.html)

```
aws ec2 describe-subnets ^
    --region eu-central-1 ^
    --profile devopsteam01 ^
    --output table ^
    --filter Name=vpc-id,Values=vpc-i346
```


### Afficher les subnets

```bash
$ aws ec2 describe-subnets --profile devopsteam01 --region eu-central-1 --output table
```

```
[OUTPUT]
------------------------------------------------------------------------------------------------------------
|                                              DescribeSubnets                                             |
+----------------------------------------------------------------------------------------------------------+
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.10.0/28                                                           ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0c409522b892fc4bf  ||
||  SubnetId                    |  subnet-0c409522b892fc4bf                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+---------------------------+--------------------------------------------------------------------------+||
|||  Key                      |  Name                                                                    |||
|||  Value                    |  subnet-10.0.10.0/28                                                     |||
||+---------------------------+--------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.4.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-02d0c07be4b48422c  ||
||  SubnetId                    |  subnet-02d0c07be4b48422c                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.4.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
```

## Add tag to an exisiting resource

* [AWS CLI - Create tags](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-tags.html)

```
aws ec2 create-tags ^
    --resources subnet-026ee5b4de5a53a01 ^
    --tags Key=Name,Value=subnet-10.0.99.0/28 ^
    --profile devopsteam01 ^
    --region eu-central-1 ^
    --output table
```

```
no input
```

## Create a private subnet

* [AWS CLI - Create Subnet](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-subnet.html)

```
aws ec2 create-subnet ^
    --vpc-id vpc-0a22d771f16ae549d ^
    --cidr-block 10.0.0.99/28 ^
    --region eu-central-1 ^
    --profile devopsteam99-i346 ^
    --output table ^
    --tag-specifications ResourceType=subnet,Tags=[{Key=Name,Value=subnet-devopsteam01}]
```

* [AWS CLI - Create Route Table](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-route-table.html)

Note : a default route table is automatically created with the subnet

```
aws ec2 create-route-table ^
    --vpc-id vpc-0a22d771f16ae549d ^
    --region eu-central-1 ^
    --profile devopsteam01 ^
    --output table ^
    --tag-specifications ResourceType=route-table,Tags=[{Key=Name,Value=rteTable-devopsteam01}]
```

```
-------------------------------------------------------------------------
|                           CreateRouteTable                            |
+------------------+----------------------------------------------------+
|  ClientToken     |  bb7d2fa8-75e5-4690-a47d-76dea6c0f42e              |
+------------------+----------------------------------------------------+
||                             RouteTable                              ||
|+---------------+--------------------------+--------------------------+|
||    OwnerId    |      RouteTableId        |          VpcId           ||
|+---------------+--------------------------+--------------------------+|
||  709024702237 |  rtb-0acd33fa1f46d6e21   |  vpc-0a22d771f16ae549d   ||
|+---------------+--------------------------+--------------------------+|
|||                              Routes                               |||
||+-----------------------+------------+--------------------+---------+||
||| DestinationCidrBlock  | GatewayId  |      Origin        |  State  |||
||+-----------------------+------------+--------------------+---------+||
|||  10.0.0.0/16          |  local     |  CreateRouteTable  |  active |||
||+-----------------------+------------+--------------------+---------+||
|||                               Tags                                |||
||+---------------+---------------------------------------------------+||
|||      Key      |                       Value                       |||
||+---------------+---------------------------------------------------+||
|||  Name         |  rteTable-devopsteam99                            |||
||+---------------+---------------------------------------------------+||
```

## Associate subnet and route table

* [AWS CLI - Association route table](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-subnet.html)

```
aws ec2 associate-route-table ^
    --route-table-id rtb-01ebe5717e9104f85 ^
    --subnet-id subnet-0fc3126df64eea2b9 ^
    --region eu-central-1 ^
    --profile devopsteam01 ^
    --output table
```

```
-------------------------------------------------
|              AssociateRouteTable              |
+----------------+------------------------------+
|  AssociationId |  rtbassoc-0edba46989de7531d  |
+----------------+------------------------------+
||              AssociationState               ||
|+----------------+----------------------------+|
||  State         |  associated                ||
|+----------------+----------------------------+|
```

* [AWS CLI - create route](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-route.html)

```
aws ec2 create-route ^
    --route-table-id rtb-01ebe5717e9104f85 ^
    --destination-cidr-block 0.0.0.0/0 ^
    --instance-id i-09d3919ca6d27ab6b ^
    --region eu-central-1 ^
    --profile devopsteam01 ^
    --output table
```

```
--------------------
|    CreateRoute   |
+---------+--------+
|  Return |  True  |
+---------+--------+
```
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
```
* [AWS CLI - create-route](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/describe-subnets.html)
```
Add table in route table
$ aws ec2 create-route --route-table-id rtb-01ebe5717e9104f85 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-059306bf876cf19f6 --profil devopsteam01 --regio eu-central-1

(An error occurred (RouteAlreadyExists) when calling the CreateRoute operation: The route identified by 0.0.0.0/0 already exists.)

```

