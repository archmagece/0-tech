# 기본 셋팅

## no password

사용자명 ALL=NOPASSWD: ALL

```
현재 사용자만 비밀번호 없이
$ echo "$USER ALL=NOPASSWD: ALL" | sudo tee -a /etc/sudoers.d/nopasswd

sudo 사용자 모두 비밀번호 없이
$ echo "%sudo ALL=NOPASSWD: ALL" | sudo tee -a /etc/sudoers.d/nopasswd
```

## change download mirror

### ubuntu
`/etc/apt/source.list`

```
$ sudo sed -i "s@kr.archive.ubuntu.com@mirror.kakao.com@g" /etc/apt/source.list
```

### mint
`/etc/apt/sources.list.d/official-package-repositories.list`

```
$ sudo sed -i "s@kr.archive.ubuntu.com@mirror.kakao.com@g" /etc/apt/sources.list.d/official-package-repositories.list
```

### manjaro
없음


