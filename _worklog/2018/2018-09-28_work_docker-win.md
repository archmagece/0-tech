# 20180918

1. 도커 접속오류
2. 도커 공유폴더 문제
3. oraclejdk8 -> openjdk10 실패

## 도커 접속오류

on
>windows10\
choco install -y docker-toolbox

### docker-for-windows 와 docker-toolbox의 차이

docker-machine 설정의 차이라고 봐야할 것 같다.

#### docker-for-windows

특징
1. HyperV와 함께 사용
1. docker-machine 사용안하는 것 같다

<pre>
$ docker -p 8080:8080 
$ curl localhost:8080
ok
</pre>

잘됨. 옛날 기억으로는...


#### docker-toolbox

구성
1. boot2docker.iso
2. docker.exe
3. docker-compose.exe
4. docker-machine.exe
5. docker-quickstart-terminal.ico
6. start.sh
7. unins000.dat
8. unins000.exe

특징
1. 도커관련 실행파일 셋
2. start.sh에서 docker-machine을 구동시켜서 도커 구성을 편하게

<pre>
$ docker -p 8080:8080 
$ curl localhost:8080
err
$ curl 192.168.99.100:8080
ok
</pre>

#### 정리

문제는 docker-machine에서 bridge-network를 구성 해 주지 않는데 있었다.\
docker run -p 0000:0000 ~~ 같은 명령어를 사용할 때\
docker-for-windows는 윈도우 host에 port를 열어줘서 localhost:0000접속이 되는데\
docker-toolbox는 접속이 안된다. toolbox에서 host는 virtualbox의 VM이다.


bridge network 추가 명령\
https://www.virtualbox.org/manual/ch06.html#network_bridged
```
VBoxManage list natnetworks

```

## 도커 공유 볼륨 문제

도커 공유폴더 문제\
docker-for-windows와 docker-toolbox에서 모두 발생했던 문제.\
오늘 확인하고 처리한 것은 docker-toolbox에서 발생한 부분


### docker-toolbox에서 docker-compose volume 설정

virtualbox에서 공유폴더 설정을 해 줘야한다.

공유폴더 지정시 다음과 같이 값을 지정
<pre>
name : d/workspace/myproject
path : D:\workspace\myproject
automount : true
</pre>

자신이 현재 사용하는 volume이름하고 경로명을 통일시켜서 해당 도커VM에 설정을 해 줘야한다.

드라이브를 통째로 잡아도 상관없겠지만 여러 vm을 돌릴 때 애매할 수 있을 것 같아서.

```
currpath : D:\workspace\myproject 인 경우
아래의 mysql 설정파일을 volume에 넣어야 할 경우

volumes:
  - ./conf/my.cnf:/etc/mysql/my.cnf
```
위의 경우 docker-compose에서 현재경로에 ./conf/my.cnf를 덧붙여서 경로 문자열을 만들어 낸다.
그럼 이런 문자열이 나올텐데 ```/cd/workspace/myproject``` 그냥 이걸 공유폴더 이름과 일치시키면 된다.

GUI에서 처리해도 되지만..terminal 명령

```
VBoxManage sharedfolder add dev --name srv --hostpath  "/my/local/path" --transient
```
https://www.virtualbox.org/manual/ch04.html#sharedfolders

참고
```
$env:COMPOSE_CONVERT_WINDOWS_PATHS=1
Set COMPOSE_CONVERT_WINDOWS_PATHS=1
```
이게 솔루션으로 제시되기도 했었는데.. 아니다. 아닌 것 같다.
아닌가? PATHS1로 잡아줘야되는건가??
내일 확인해보고


### docker-for-windows에서 docker-compose volume 설정

아직 해결 못함


## jdk10 호환성 문제

<pre>
scoop install openjdk10
scoop install ojdkbuild8
</pre>

jdk10시 출시됐다고 하고 scoop에서 openjdk 기본설치가 10을 지원하길래 생각없이 설치했다가!!

버전업은 항상 거대한 희생이 따른다.

1. kotlin에서 10을 지원 해 주지 않는다. 현재 최신인 kotlin 1.2.71에서도 1.8까지 지원
2. gradle 낮은 버전에서 지속적으로 오류가 발생한다. 4.9이상 버전사용
3. lombok에서 오류. querydsl하고 함께 사용해야 하는데 곤란하다.

가장 큰 문제는 로그에서 문제라고 잘 뜨지도 않는다.

jdk10에서 새로생긴 기능이 뭔지도 잘 모르겠고... 현대 java보다 kotlin을 더 많이 쓰기 때문에 jdk8버전으로 다운. 해결