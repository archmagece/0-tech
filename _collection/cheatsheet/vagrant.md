
# Vagrant

## 사용법

### Vagrant ssh 접속

1 ssh 접속 설정\
~/.ssh/config
``` text
Host 192.168.56.101
  IdentifiyFile ~/.vagrant.d/insecure_private_key
  User vagrant
```

2 vagrant ssh-confg 사용
```
vagrant ssh-config --host default >> ~/.ssh/config
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /home/archmagece/work/infra/cheftet/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL
```

### 명령어 실행

config.vm.provision :shell, path: "install.sh"
config.vm.provision :reload
config.vm.provision :shell, path: "start.sh"

## plugins

### scp

``` bash
vagrant plugin install vagrant-scp
vagrant scp <some_local_file_or_dir> [vm_name]:<somewhere_on_the_vm>
vagrant scp ~/Download/default/chefdk_3.1.0-1_amd64.deb default:~
```


### sahara
```
vagrant plugin install sahara
```

``` bash
vagrant sandbox on

vagrant sandbox rollback

vagrant sandbox commit

vagrant sandbox off
```

### chef plugins


### vagrant-disksize
vagrant plugin install vagrant-disksize

### vagrant-reload
vagrant plugin install vagrant-reload

### vagrant-vbguest
vagrant plugin install vagrant-vbguest

### vagrant-docker-compose
vagrant plugin install vagrant-docker-compose

### vagrant-hostmanager
vagrant plugin install vagrant-hostmanager
https://github.com/purpleidea/vagrant-hostmanager/

### vagrant-libvirt
vagrant plugin install vagrant-libvirt
https://github.com/vagrant-libvirt/vagrant-libvirt

## boxes
debian10: debian/buster64
  debian/buster64
  
debian9: debian/stretch64
  debian/stretch64
  bento/debian-9.8
debian8: debian/jessie64
  debian/jessie64
debian7: debian/wheezy64
  debian/wheezy64
debian6: debian/squeeze64
  debian/squeeze64

ubuntu12.04: precise pangolin
  ubuntu/pangolin64
  bento/ubuntu12.04
ubuntu14.04: trusty tahr
  ubuntu/trusty64
  bento/ubuntu14.04
ubuntu16.04: xenial xerus
  ubuntu/xenial64
  bento/ubuntu16.04
ubuntu18.04: bionic beaver
  ubuntu/bionic64
  bento/ubuntu18.04

centos
  bento/centos-6.8
  bento/centos-7.2
  bento/centos-7.6

fedora
  bento/fedora-22
  bento/fedora-27

freebsd
  bento/freebsd-12

opensuse
  bento/opensuse-leap-15

## 참고사이트
https://github.com/iJackUA/awesome-vagrant