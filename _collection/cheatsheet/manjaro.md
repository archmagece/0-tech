# manjaro linux
문서화가 잘되어 있다
wiki.manjaro.org

기본설치

## pacman
```
$ sudo pacman -Syyu
$ sudo pacman -Syup

sudo pacman -Su --noconfirm
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

## packages

(internet)
chromium filezilla transmission-remote-gtk

(editor)
atom code kate

(terminal)
guake neovim xfce4-terminal

(note)
knotes gnote

(file manager)
krusader krename kdiff3 lha arj unarj unace
nextcloud-client

(keybodard)
ibus-typing-booster 


(calculator)
wxmaxima

(messenger)
telegram-desktop

(dev)
wireshark-gtk nmap
qgis r kitty virtualbox

sudo pacman -S base-devel --needed

yaourt synology-cloud-station-drive

