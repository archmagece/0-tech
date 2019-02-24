# manjaro linux
문서화가 잘되어 있다
wiki.manjaro.org

기본설치

## pacman
```
$ sudo pacman -Syyu
```

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

yaourt -S ttf-nanum noto-fonts-cjk
pacman -S terminus-font noto-fonts-cjk ttf-dejavu

### ibus
~/.bashrc
```
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
```

### fcitx


### nimf

yaourt -S nimf

```
export GTK_IM_MODULE="nimf"
export QT4_IM_MODULE="nimf"
export QT_IM_MODULE="nimf"
export XMODIFIERS="@im=nimf"
nimf
```
nimf-daemon
nimf-indicator