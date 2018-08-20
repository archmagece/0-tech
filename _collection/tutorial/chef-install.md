---
layout: post
title:  "Chef, Infrastructure as Code"
date:   2018-08-01 14:41:00 +0900
categories: infra
---

# Chef를 이용한 인프라 자동화

## 실습 환경

Ubuntu Desktop 18.04\
Virtualbox\
Vagrant Ubuntu 16.04

## 개념

Chef DK - Server + Client

Chef Solo

https://docs.chef.io/chef_repo.html

## Keyword

Cookbook, Resource, Attribute, Data Bags, Environment, Provider, LWRP, Kitchen

### Resource

https://docs.chef.io/resource_reference.html

package, log


## 설치

### Vagrant 환경

#### Vagrantfile 기본설정

``` vagrant
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

접속

``` bash
vagrant init
vagrant up
vagrant ssh
```

### ruby 설치 - rbenv

#### rbenv 설치

``` bash
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build

echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
```

#### ruby 설치

``` bash
rbenv install 2.5.1
rbenv global 2.5.1
# CC=/usr/bin/gcc-4.8 rbenv install 2.3.3
gem install bundler
```

### chef solo 설치

``` bash
gem install chef
chef-solo --version
Chef: 14.3.37
```

### chef dk 설치

chef solo는 심플 클라이언트 느낌이고 풀 버전은 dk설치

git global 설정. 안해주면 두고두고 오류발생
```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

## testlog

### knife 명령어로 쿡북 생성

knife 기본 설정\
`knife configure`\
테스트시에는 기본설정으로 셋팅

``` bash
chef generate cookbook hello
```

### 패키지 설치

zsh 설치

``` chef
package "zsh" do
  action :install
end
```
여러개 패키지 설치

``` chef
%{zsh gcc make readline-devel}.each do |pkg|
  package pkg do
    action :install
  end
end
```

루비 코드를 이용해서 처리할 수 있고
chef에서 os랑 알아서 처리 해 준다.f


### 복잡한 쿡북

`chef generate cookbook nginx_cookbook`

``` bash
├── Berksfile
├── CHANGELOG.md
├── chefignore
├── LICENSE
├── metadata.rb
├── README.md
├── recipes
│   └── default.rb
├── spec
│   ├── spec_helper.rb
│   └── unit
│       └── recipes
│           └── default_spec.rb
└── test
    └── integration
        └── default
            └── default_test.rb
```

디렉토리 용도

```
recipes/
templates/ 템플릿 파일 erb
files/ 파일 저장
attributes/ 변수의 기본 값을 설ㅈ어
```


nginx_cookbook/recipes/default.rb

``` chef
package "nginx" do
  action :install
end

service "nginx" do
  supports :status => true, :restart => true, :reload => true
  action [:enable, :start]
end

template "nginx.conf" do
  path "/etc/nginx/nginx.conf"
  source "nginx.conf.erb"
  owner "root"
  group "root"
  mode 0644
  notifies :reload, 'service[nginx]'
end
```

nginx_cookbook/templates/default/nginx.conf.erb

``` erb
user nginx;
worker_processes 1;
error_log /var/log/nginx/error.log;
pid /var/run/nginx.pid;

events{
  worker_connections 1024;
}

http {
  include /etc/nginx/mime.types;
  default_type application/octet-stream;

  server {
    listen <%= node['nginx']['port'] %>;
    server_name localhost;
    location / {
      root /usr/share/nginx/html;
      index index.html index.htm;
    }
  }
}
```

위의 설정데이터 저장\
chef server이용하는 경우 서버에 저장이 되어 있는데\
solo는 로컬에서 실행시켜야 되서 설정정보 json에 저장\
nginx_cookbook.json

``` json
{
  "nginx":{
    "port": 80
  },
  "run_list"[
    "nginx"
  ]
}
```

nodes/ 설정 json파일 저장

Repositoy 생성

`chef generate repo testrepo`

```
├── chefignore
├── cookbooks
│   ├── example
│   │   ├── attributes
│   │   │   └── default.rb
│   │   ├── metadata.rb
│   │   ├── README.md
│   │   └── recipes
│   │       └── default.rb
│   └── README.md
├── data_bags
│   ├── example
│   │   └── example_item.json
│   └── README.md
├── environments
│   ├── example.json
│   └── README.md
├── LICENSE
├── README.md
└── roles
    ├── example.json
    └── README.md
```

여러 호스트에서 knife 실행

`echo user@node1 user@node2 user@node3 | xargs -n 1 chef-solo cookbook`


## cookbooks

### td-agent

``` ruby
#td-agent 그룹 생성
group 'td-agent' do
  group_name 'td-agent'
  gid 403
  action [:create]
end
#td-agent 사용자 생성
user 'td-agent' do
  comment 'td-agent'
  uid 403
  group 'td-agent'
  home'/var/run/td-agent'
  shell '/bin/false'
  password nil
  supports :manage_home => true
  action [:create, :manage]
end
#디렉토리생성
directory '/etc/td-agent' do
  owner 'td-agent'
  group 'td-agent'
  mode '0755'
  action :create
end
# 리포지토리 연결
## node['platform']은 Attribute.
## attribute는 ohai를 이용 확인
## ex) ohai | grep platform
## ex) ohai platform
case node['platform']
when 'ubuntu'
  dist = node['lsb']['codename']
  source = (dist == 'precise') ? "http://packages.treasure-data.com/precise/" : "http://packages.treasure-data.com/debian/"
  apt-repository 'treasure-data' do
    uri source
    distribution dist
    components ['contrib']
    action :add
  end
when 'centos', 'redhat'
  yum_repository 'treasure-data' do
    url "http://packages.treasure-data.com/redhat/$basearch"
    action :add
  end
end
# 설정 파일을 생성
template "/etc/td-agent/td-agent.conf" do
  mode "0644"
  source "td-agent.conf.erb"
end
# 패키지 설치
package "td-agent" do
  options "-f --force-yes"
  action :upgrade
end
# 서비스 활성화
service "td-agent" do
  action [:enable, :start]
  subscribes :restart, resources(:template => "/etc/td-agent/td-agent.conf")
end
```

### package 설치

```ruby
package "nginx" do
  action :inatsll
  version "x.x.x"
end
package "apache" do
  action :remove
end
package "tar" do
  action :install
  source "/tmp/tar-x.x.x.rpm"
  provider Chef::Provider::Package::Rpm
end
gem_package "rails" do
  action :install
end
#td-agent gem을 설치.
gem_package 'fluent-plugin-extract_query_params' do
  gem_binary "/usr/lib64/fluent/ruby/bin/fluent-gem"
  version '0.0.2'
  action :upgrade
end
```

## notification

기본적으로 이벤트 발생시 큐에 쌓아줬다가 모든 처리가 끝난 후 처리
:immediately 셋팅으로 즉시 실행 가능

### 이벤트 발생시 리소스 호출

nginx 설정파일 변경시 서비스 리로드

```ruby
#nginx 서비스 활성화
service "nginx" do
  supports :status => true, :restart => true, :reload => true
  action [:enable, :statrt]
end

#템플릿변경시 트리거
template "nginx.conf" do
  path "/etc/nginx/nginx.conf"
  source "nginx.conf.erb"
  owner "root"
  group "root"
  mode 0644
  notifies :reload, 'service[nginx]'
end
```

### 어떤 리소스가 동작되는 경우 수신

```ruby
service "td-agent" do
  supports :status => true, :restart => true, :reload => true
  action [:enable, :start]
  subcribes :restart, "template[td-agent.conf]"
end
```

## cookbookfile

`cookbook_root/files/default/supervisor-3.0a12-xxx.rpm` 파일을 전송

```ruby
cookbook_file "/tmp/supervisor-3.0a12-xxx.rpm" do
  mode 0644
end
#같은표현
cookbook_file "/tmp/supervisor-3.0a12-xxx.rpm" do
  soruce "supervisor-3.0a12-xxx.rpm"
  mode 0644
end
cookbook_file "/tmp/supervisor-3.0a12-xxx.rpm" do
  soruce "supervisor-3.0a12-xxx.rpm"
  mode 0644
  checksum "012jf93j0ur03rj03jf03jt3jxxxxxxxxx"
end
```
파일 체크섬은 `shasum -a 256 supervisor-3.0a12-xxx.rpm` 명령으로 생성

## Deploy

### git

```ruby
git "/home/vagrant/.oh-my-zsh" do
  repository "git://github.com/robbyrussell/oh-my-zsh.git"
  reference "master"
  # 매번 갱신하려면 sync
  action :checkout
  user "aaaaa"
  group "aaaaa"
end
```

## bash
```ruby
bash "install perlbrew" do
  user 'vagrant'
  group 'vagrant'
  # current work directory
  cwd '/home/vagrant'
  # 환경변수 셋팅
  environment "HOME" => '/home/vagrant'
  code <<-EOC
    curl -kL http://install.perlvrew.pl | bash
  EOC
  # 지정한 파일을 생성하고 있을경우 실행하지 않는다
  creates '/home/vagrant/perl5/perlbrew/bin/perlbrew'
  # not if 지정한 조건이 참이 아닐 때 명령어를 실행
  not_if {File.exists? ("/home/vagrant/perl5/perlbrew/bin/perlbrew")}
  not_if 'which ruby'
  # only_if 지정한 조건이 참일 때 명령어를 실행
end
```

## Cron

```ruby
cron "name_of_cron_entry" do
  hour 8
  weekday 6
  mailto admin@opscode.com
  action :create
end
```

## File

## http_request

## ifconfig

```ruby
ifconfig "192.168.0.1" do
  device "eth0"
end
```

## Link

## Mount

## Route

## ruby_block

ruby 코드를 실행하기 위한 블록

```ruby
ruby_block "reload_client_config" do
  block do
    Chef:Config.from_file("/etc/chef/client.rb")
  end
  action :create
end
```


## run_list

```json
{
  "run_list":[
    "nginx",
    "apache2"
  ]
}

{
  "run_list":[
    "nginx::default",
    "apache2",
    "apache2::mod_ssl"
  ]
}

{
  "run_list":[
    "recipe[nginx::default]",
    "recipe[apache2]",
    "recipe[apache2::mod_ssl]"
  ]
}

{
  "run_list":[
    "recipe[yum::epel]",
    "role[webserver]"
  ]
}
```

## custom resource 정으

Definition으로 cpanm의 Resource를 정의


LWRP(Lightweight Resource and Providers)

## Attribute 정의

json파일에 정의

```json
{
  "nginx":{
    "port":80
  },
  "run_list":[
    "~~"
  ]
}
```

attributes/default.rb

```ruby
default["apache"]["dir"] = "/etc/apache2"
default["apache"]["listen_ports"] = ["80", "443"]
```

초기가ㅂㅅ 지정
role별 지정
json파일로 노드별로 지정

## data bag

글로벌 설정파일 관리 등

## berkshelf

```bash
cd chef-repo
#gitignore에 vendor 디렉터리 추가
bundle --path vendor/bundle
```

Berksfile 생성

`bundle exec berks --path cookbooks`

## chef server

## capistrano

