# Lamda with go

rds 인증방식부터 고려 필요
다른 디비면 별도 인증방법이필요

접속허용을 어디까지 해야할지 애매하니까

## lambda rds 인증
https://docs.aws.amazon.com/ko_kr/AmazonRDS/latest/UserGuide/UsingWithRDS.IAMDBAuth.Enabling.html
```mysql
CREATE USER 'lambda_user' IDENTIFIED WITH AWSAuthenticationPlugin as 'RDS';
GRANT ALL PRIVILEGES ON aph_aiprediction_db.* TO 'lambda_user'@'%';
FLUSH PRIVILEGES;
```

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "rds-db:connect"
            ],
            "Resource": [
                "arn:aws:rds-db:ap-northeast-2:611690826646:lambda_user:db-2XDEODHCBCHOIKXC3DZDBRVWAQ/db_user"
            ]
        }
    ]
}
```

## 코드
https://docs.aws.amazon.com/sdk-for-go/api/aws/credentials/