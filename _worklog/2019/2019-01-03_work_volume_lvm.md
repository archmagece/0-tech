# 우분투 lvm 추가제거

개발용 우분투 피씨 용량이 부족해서 서버로 쓰던 컴퓨터 lvm잡혀있던 하드를 빼왔다

내용물이 뭐가 있는지 제대로 확인을 안했네..

## 개념

https://access.redhat.com/documentation/ko-kr/red_hat_enterprise_linux/6/html/logical_volume_manager_administration/

우분투와 같지는 않지만 리눅스 시스템 구조는 비슷하니까

레이드 거는거랑 비슷한 개념이라고 보면 되는데 논리적으로 거는 개념이다.

여러개의 하드를 그냥 연결 해 놓고

한개는 아니지만 한개의 드라이버인 것 처럼 사용한다거나

레이드보다 더 불안정한 상태로 날라가도 되는 드라이버인 경우 쓰기 좋은거 아닐까

## LVM 만들기
0. fdisk 파티션 생성
1. pv(physical volume)
2. vg(volume group)
3. lv(logicla volume)

### 파티션 생성
파티션 확인
```
$ sudo fdisk -l
~~~
Disk /dev/nvme0n1: 119.2 GiB, 128035676160 bytes, 250069680 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: ACE51371-D9DE-4B56-8EED-9E26986CF3BD

Device         Start       End   Sectors   Size Type
/dev/nvme0n1p1  2048 250068991 250066944 119.2G Linux filesystem


Disk /dev/sda: 465.8 GiB, 500107862016 bytes, 976773168 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: CC6F5D8A-8870-400F-A80B-4ECA0B7B7AC8
~~~
```

$ sudo lsblk

$ sudo fdisk /dev/sdb
$ sudo fdisk -l /dev/sdb
$ sudo fdisk /dev/sdc
$ sudo fdisk -l /dev/sdc

$ sudo mkfs.ext4 /dev/sdb1
$ sudo mkfs.ext4 /dev/sdc1

### pv

```
$ sudo pvdisplay
$ sudo pvcreate 파티션 파티션 파티션 ...
$ sudo pvcreate /dev/sdb1 /dev/sdc1
$ sudo pvdisplay
```

### vg

```
$ sudo vgdisplay
$ sudo vgcreate 볼륨그룹이름 파티션 파티션 파티션 ...
$ sudo vgcreate vg0 /dev/sdb1 /dev/sdc1
$ sudo vgdisplay
```

### lv

```
$ sudo lvdisplay
$ sudo lvcreate -L 용량 -n 로지컬볼륨이름 볼륨그룹이름
$ sudo lvcreate -n lv0 -L 80g vg0
$ sudo lvcreate -n lv0 -l 100%FREE vg0
$ sudo lvdisplay
```

### 마운트

테스트
```
sudo mkdir /datadir
sudo mount -t /datadir
df -h
sudo unmount /datadir
```

sudo blkid

/etc/fstab 등록
```
/dev/mapper/vg0
```

## LVM 용량추가

fdisk -l /dev/sdb
fdisk -l /dev/sdc
새로한개 더 추가할거
fdisk -l /dev/sdd

pvcreate /dev/sdd1
vgextend vg0 /dev/sdd1

vgdisplay


## LVM 용량제외

vgremove /dev/sdd1
vgdisplay
lvdisplay

## LVM 완전삭제

pvremove /deb/sdb1
pvremove /deb/sdc1
pvremove /deb/sdd1

sudo lvremove lv0
sudo vgremove vg0