# lmv 볼륨설정



## 세개 디스크 lvm 파티션 만들기

/dev/sdb
/dev/sdc
/dev/sdd

fdisk 이용 디스크 목록 보기
sudo fdisk -l

하나씩 파티션 정리
``` command
sudo fdisk /dev/sdb
```
끝나면 나머지 이어서
sudo fdisk /dev/sdc
sudo fdisk /dev/sdd

Command (m for help):

n = create new partition
p = creates primary partition
1 = makes partiton the first on the disk

새 파티션 만들기
``` command
n
```


t = change partition type
31 = changes to LVM partition type

파티션 타입 LVM 설정
``` command
t
31
```

p = view partition setup
w = write chagnes

지금까지 설정한거 확인하고 종료
``` command
p
w
```

## LVM 그룹 설정

### PV(Physical Volume) 생성

sudo pvcreate {디스크경로}
sudo pvcreate /dev/sdb1
sudo pvcreate /dev/sdc1
sudo pvcreate /dev/sdd1

pv생성 확인
sudo pvscan

### VG(Volume Group) 생성

vgcreate {볼륨그룹이름} {볼륨} {볼륨}
vgcreate vgtank /dev/sdb1 /dev/sdc1 /dev/sdd1

그룹생성 확인
sudo vgscan
sudo vgdisplay


### LV(Logical Volume) 생성

sudo lvcreate -L {용량} -n {로지컬볼륨이름} {아까만든 볼륨그룹이름}
sudo lvcreate -L 3G -n lvtank vgtank
sudo lvcreate -L 10%VG -n lvtank vgtank
sudo lvcreate -L 100%FREE -n lvtank vgtank



## 포맷

sudo mkfs.ext4 {드라이브 경로}
sudo mkfs.ext4 /dev/mapper/vgtank-lvtank


## 디스크 마운트

### 수동마운트

sudo mkdir {마운트 디렉토리 이름}
sudo mkdir /tank

sudo mount -t ext4 /dev/mapper/{볼륨그룹이름}-{로지컬볼륨이름} {마운트 디렉토리 이름}
sudo mount -t ext4 /dev/mapper/vgtank-lvtank /tank

### 수동마운트 확인

df -h

아까 잡아놓은 용량이 보이면 성공


https://serverfault.com/questions/174181/how-do-you-validate-fstab-without-rebooting


/etc/fstab


설정후

sudo mount -a

https://serverfault.com/questions/174181/how-do-you-validate-fstab-without-rebooting

