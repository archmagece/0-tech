# aws tag name 정하기

## stage
개발 단계별 네이밍

1. tmp temporal
1. dev develop
1. aph alpha
1. stg staging
1. prd production

### temporal
임시로 사용후 삭제
주말에 인프라 관리자가 임의삭제할지도 모름

### develop
개발단계. 지속으로 배포 테스트
개발 관계자 테스트 환경

### alpha
실무자/기획자/다른개발자 테스트단계
실제와 비슷한 환경
버전별 분리
feature, bug, improvement 항목별 주소 별도 생성

패턴은 정의 필요
{module_name}-aph.app-domain.tld/{versioncode}
{module_name}-{versioncode}-aph.app-domain.tld/

### staging
production의 복제환경

쉽게 리셋가능하도록.
필요시 production 환경을 복제해서 가졍로 수 있도록 셋팅

### production
최종 서비스 환경

## 서비스 네이밍 규칙

{state}_{서비스내에서이름}_{aws서비스명}
dev_서비스명_dokku_ec2
dev_dokku0_ec2
dev_default_vpc
dev_inoffice_secgrp
dev_서비스명_subnet
aph_서비스명_eks

rds/ec2/eks/vpc/secgrp/subnet

## 태그 네이밍 규칙

Stage=dev/aph/stg/prd/tmp
Owner=자기사업부명/팀명
Project=프로젝트명
Module=프로젝트모듈명