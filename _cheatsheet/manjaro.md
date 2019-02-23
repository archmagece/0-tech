# manjaro linux
문서화가 잘되어 있다
wiki.manjaro.org

기본설치


## ntp
wiki/System_Time_Setting

### 상태확인
```
$ timestaectl
$ timedatectl status
$ date
```
## 설치
```
$ sudo pacman -S ntp
$ 
$ timedatect set-ntp true
```

## 한글

### ibus
~/.bashrc
```
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
```

