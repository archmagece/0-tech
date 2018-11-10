# Ansible

## 설치
pip install ansible




## 설정

설정파일 위치
/etc/ansible


/etc/ansible/hosts
```env
[webservers]
site01
site02
site01-dr

[production]
site01
site02
db01
bastion
```

## 실행

서버연결 체크
`ansible site01 -u root -k -m ping`

.ssh/config 설정 후
사용자명 -u root
비밀번호 -k
SUDO -K
생략가능

`ansible site01 -m ping`

서버연결 결과
```
site01 | success >> {
    "changed": false,
    "ping": "pong"
}
```

remote_user
remote_port
ansible_ssh_user

```env
[webservers]
site01 ansible_ssh_user=root
site02 ansible_ssh_user=daniel
site01-dr ansible_ssh_host=site01.dr ansible_ssh_port=65422
[production]
site01
site02
db01 ansible_ssh_user=archmagece ansible_ssh_private_key_file=/home/archmagece/.ssh/id_rsa bastion
```


장비에 setup 모듈실행
`ansible <machine name> -m setup`
`ansible <machine name> -m file a 'path=/etc/fstab'`

```
-m copy
-m command
-m shell
```

모듈 정보 찾아보기
ansible-doc -l
ansible-doc file


