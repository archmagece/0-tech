# 소프트웨어 raid

상태확인
lsblk

cat /proc/mdstat

mdadm --create --verbose /dev/md0 --level=0 --raid-devices=2 /dev/sda /dev/sdb

cat /proc/mdstat

sudo mdadm --detail --scan

mkfs.ext4 /dev/md0


마운트
mkdir /datadir
mount -t /dev/md0
mount -t /dev/md127

md127은 어디서 온걸까..
어느순간 md0라는 이름이 없어져 있고 127로 변경 돼 있었다.
/etc/mdadm.conf에 설정을 해줘야 한다는 것 같은데
서버도 아니고 로컬환경에서 127로 써도 상관없지 않을까


fstab에는 
/dev/md127 /datadir ext4 defaults 0 0

대충됐으니 완료.