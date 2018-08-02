---
layout: post
title:  "Chef, Infrastructure as Code"
date:   2018-08-01 14:41:00 +0900
categories: infra
---

# Chef를 이용한 인프라 자동화

## 실습 환경

Ubuntu Desktop 18.04
Virtualbox
Vagrant Ubuntu 16.04

## 개념

Chef Server+Client
Chef Solo

## Keyword

Cookbook, Resource, Attribute, Data Bags, Environment, Provider, LWRP, Kitchen

## 설치

셰프 솔로
gem install chef

제대로 설치하려면 deb 파일 다운


## Test Log

```vagrant
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network 'private_network', ip: '192.168.56.101', name: 'vboxnet0'

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get upgrade -y
    apt-get install -y  autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm3 libgdbm-dev git
    # runuser -l vagrant -c 'git clone https://github.com/rbenv/rbenv.git ~/.rbenv'
  SHELL
end
```

vagrant up
vagrant ssh


rbenv 설치 1
`sudo apt-get install -y rbenv`

rbenv 설치 2
```
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build

echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
```

ruby 설치
```
rbenv install 2.5.1
rbenv global 2.5.1
# CC=/usr/bin/gcc-4.8 rbenv install 2.3.3
gem install bundler
```

chef 설치
chef solo
`gem install chef`

chef dk




### knife 명령어로 쿡북 생성

knife configure

