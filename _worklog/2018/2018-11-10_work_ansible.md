# Ansible

## 설치
pip install ansible


## 설정


```bash
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

서버연결 실행

`ansible site01 -u root -k -m ping`

서버연결 결과
```
site01 | success >> {
    "changed": false,
    "ping": "pong"
}
```

ssh키 설정이 돼 있으면 -k 생략


사용자 이름
/etc/ansible/ansible.cfg

remote_user
remote_port
ansible_ssh_user
