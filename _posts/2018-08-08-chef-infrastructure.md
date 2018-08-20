---
layout: post
title:  "Infra - Chef를 이용한 운영/테스트 환경 자동화"
date:   2018-08-08 13:00:00 +0900
categories: jekyll update
---

# Chef

## 왜 쓰나

컨테이너의 시대에 이걸 왜 쓸까?

사실 배포는 거의 컨테이너(도커)를 이용한다. 그래도 dokku, HAproxy, gw 등을 별도로 구성해야 할 일이 종종 있다.
hadoop, yarn 등도...
요즘은 jenkins도 kubernetes에 배포하기도 하지만 독립 인스턴스로 하는것도 괜찮을 것 같고

infra as code. 소스코드처럼 서버를 관리할 수 있다. 클라우드 환경에서는 물론이고 로컬 개발서버 구성시에도 쉽게 초기화가 가능하다.

## 특징

멱등성을 보장하는 인프라 관리 언어

요즘은 컨테이너에 밀려 주춤하지만..
모든걸 다 컨테이너에서 구성하진 못 하니 개발서버 관리. 서버설치 등에 사용하면 좋다.

컨테이너에 밀려 주요 서비스 배포에는 사용되지 않지만
컨테이너 서버 구성, 프록시 서버 설치, 등등 여러 용도로 사용가능하다.

로컬에서도 컨테이너 말고 vagrant+virtualbox를 이용해서 테스트 환경을 구성하는 경우도 있으니까

# 맛보기

## 개념

워크스테이션(로컬피씨) - 서버

chef - chef 클라이언트
knife - chef 서버접속용 클라이언트
chef-dk - chef 로컬환경

chef supermarket
chef private(hosted)
vagrant
onmibus
sahara

## 준비

루비 설치 - chef gem설치

쿡북을 만들려면 chef - dk 설치

chef.io 가입

knife 초기화

vagrant 설치, omnibus, sahara, butcher 설치

## 따라하기

### 설치

1. virtualbox 설치\
os에 따라서 다른데 sudo apt install virtualbox

1. 테스트 디렉토리 생성
mkdir ~/tmp/test

1. chef.io 가입 및 설정\
이동. management console\
Administration - Organizations - Select Or Create Organizatoin - Starter Kit
다운로드 해서 압축풀면 chef-repo 작업디렉토리로 사용\
`$ cd chef-repo`\
`chef-repo/.chef` 디렉토리에 knife.rb, [username].pem 파일이 있다\
제대로 설치되었나 확인\
`knife client list`

1. vagrant 이미지 만들기\
`$ vagrant box add bento/ubuntu-18.04`\
https://github.com/chef/bento\
http://chef.github.io/bento/

2. Vagrantfile 만들고 수정\
`$ vatrant init`\
`$ nano Vagrantfile`

Vagrantfile
```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-16.04"
  # config.vm.box_url = "https://vagrantcloud.com/bento/boxes/ubuntu-16.04/versions/201807.12.0/providers/virtualbox.box"
  config.omnibus.chef_version = :latest

  config.vm.provision :chef_client do |chef|
    chef.provisioning_path = "/etc/chef"
    # 변경가능성 있음
    chef.chef_server_url = "https://chef.io/organization/{your_org_name}"
    chef.validation_key_path = ".chef/{your_username}.pem"
    chef.validation_client_name = "{your_org_name}-validator"
    chef.node_name = "server"
  end
end
```

`$ vagrant up`\
`$ vagrant ssh`

`$ knife client list`

1. 다 지우고 종료하기\
`$ vagrant destroy`\
`$ knife node delete server -y && knife client delete server -y`


### 쿡북 이용 설치 제거

iptables 커뮤니티 쿡북 설치
knife cookbook site install iptables
iptable 쿡북 업로드
knife cookbook upload iptables

knife cookbook show iptables

### 쿡북 의존성 정의

metadata.rb
berkshelf

### 앗!!

그런데 셰프 살 돈이 없다!!!

오픈소스도 아니고 완전유료라서.

puppet, ansible 등등 다 유료.

fabric을 쓰는게 낫겠다.

chef는 이만...

chef-solo는 쓸까 했는데 오픈소스인줄알았는데..

이 회사에 의존적으로 만들어놓으면 solo도 언제쯤 끊기거나 변경될지 모르고

지금도 엄청바뀌어서. 옛날책들 그대로 하면 다 먹통인데 얼마나 더 바뀔지
