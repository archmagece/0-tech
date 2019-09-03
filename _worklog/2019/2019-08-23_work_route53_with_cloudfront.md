route53 cloudfront 연결
======================

# Setting

## route53 등록

* 호스팅 영역 생성
* AWS 네임서버 생성된것 확인
* 도메인 등록업체에 AWS 네임서버 등록

## s3 리소스 생성

* s3 버킷 생성
* s3 업로드
* 권한설정 public

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowPublicReadAccess",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::simkung-becl-web-hosting/*"
        }
    ]
}
```

## aws certificate
Don't worry about price.. It's acceptable. $0.75 per month.

* add your domain

## cloudfront

* create for web
* origin domain name : s3 bucket name
  and default value
* register cname, you want register in route53

## route53 설정

* A record with alias for cloudfront name {dxxxxxx.cloudfront.net}

# Confirm Access

## 403??

cloudfront
https://aws.amazon.com/ko/premiumsupport/knowledge-center/s3-website-cloudfront-error-403/

