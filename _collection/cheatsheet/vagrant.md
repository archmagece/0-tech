
# Vagrant



## plugins

### scp

``` bash
vagrant plugin install vagrant-scp
vagrant scp <some_local_file_or_dir> [vm_name]:<somewhere_on_the_vm>
vagrant scp ~/Download/default/chefdk_3.1.0-1_amd64.deb default:~
```

#### Vagrant ssh 접속

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

### chef omnibus


