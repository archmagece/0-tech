Beanstalk
=========

```
eb create \
--vpc.id vpc-039872a4ab006ab38 \
--vpc.securitygroups sg-0eeb0162a728352c6,sg-0d74d4d21899b40c3 \
--vpc.elbsubnets subnet-03e4a2037ac9b59a4,subnet-003f5a662e1b3c0b8 \
--vpc.ec2subnets subnet-03e4a2037ac9b59a4,subnet-003f5a662e1b3c0b8 \
--vpc.dbsubnets \
--region ap-northeast-2 \
--keyname mex-env \
--platform node.js \
--sample \
--single \
mex-env4
```
ERROR: InvalidOptionsError - You can't use the "--single" argument with the "--vpc.elbsubnets" or "--vpc.elbpublic" arguments.

```
eb create \
--vpc.id vpc-039872a4ab006ab38 \
--vpc.securitygroups sg-0eeb0162a728352c6,sg-0d74d4d21899b40c3 \
--vpc.ec2subnets subnet-03e4a2037ac9b59a4,subnet-003f5a662e1b3c0b8 \
--keyname mex-env \
--platform node.js \
--sample \
--single \
mex-env4
```


소스코드에 포함시키기
https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/using-features.managing.vpc.html

.ebextensions/vpc.config
```
option_settings:
   aws:ec2:vpc:
      VPCId: vpc-087a68c03b9c50c84
      AssociatePublicIpAddress: 'true'
      ELBScheme: public
      ELBSubnets: subnet-0fe6b36bcb0ffc462,subnet-032fe3068297ac5b2
      Subnets: subnet-0fe6b36bcb0ffc462,subnet-032fe3068297ac5b2
```