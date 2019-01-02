# golang

## 특징

오버로딩 안됨. 함수 이름 다르게

## duck typing

golang은 duck typing 사용

꽥꽥거리는건 오리다

변수와 메서드를 같은걸 가지고 있으면 같은 타입이다.

## 설치

쉽다

## 문서

dodoc.org
```
godoc -http:=8080
godoc fmt Printf
godoc image/png
```

## 포매팅 도구

gofmt -h

## go의 키워드

keywords\
https://golang.org/ref/spec#Keywords¶
```
break        default      func         interface    select
case         defer        go           map          struct
chan         else         goto         package      switch
const        fallthrough  if           range        type
continue     for          import       return       var
```

reserved words\
:이 부분은 따로 정리된건 아니고 변수명이나 기타
```
append copy int8 nil true
bool delete int16 panic uint
byte error int32 print uint8
cap false int64.......
```


## 내장함수

close
len
cap
new
make
copy
append
panic, recover
complex, real, imag

## 클로저 closure

바로 호출가능한 익명함수

```
func(x, y int) int{
    return x + y
}(3, 4)
```

## 함수 파라미터

func callback(y int, fn0 func(int, int)) {
    fn0(y, 5)
}

func add(a, b int){
    fmt.Println("%d + %d = %d\n", a, b, a+b)
}

func main(){
    callback(5, add)
}


## bool

0, nil이 false로 취급되지 않는다.
오류 발생.

## 숫자

### 정수

int8
int16
int32
int64
int
uint8
uint16
uint32
uint64
uint
byte uint8의 별칭
rune int32의 별칭
uintptr  uint와 같음 포인터를 저장

10진수 = 8진수 = 16진수
365 = 0555 = 0x16D

### 문자표기

정수 타입과 문자 타입을 구분하지 않는다.

byte uint8의 별칭으로 1바이트로 표현할 수 있는 ascii문자 표기
rune int32의 별칭으로 유니코드(UTF-8) 문자를 표기

```
A
ch0 := 65
ch1 := 0101
ch2 := 0x41
ch3 := 'A'

가
ch0 := 44032
ch1 := 0126000
ch2 := 0xAC00
ch3 := '가'
```

### 실수

float32 소수점7자리
float64 소수점15자리

### 복소수

complex64 32비트의 실수부와 허수부
complex128 64비트의 실수부와 허수부


```
c1 := 1 + 2i    //complex128
c2 := complex64(3 + 4i)    //complex64
c3 := complex(5, 6)    //complex128

real(c1), imag(c1)
real(c2), imag(c2)
real(c3), imag(c3)
```

복소수 연산 - math/cmplx 패키지

### 숫자의 연산

자동형변환 안됨. 형변환시에 대충되는거 없고 불가능할 경우에는 에러 발생


공식문서 링크
모든숫자 타입에 사용가능연산자

공식문서 링크
정수 타입에만 사용가능한 연산자


## 문자열 관련

ch3, 공식문서 링크

## 배열과 슬라이스

슬라이스는 리스트처럼 가변길이

cap 배열/슬라이스의 용량 (배열은 길이와 용량이 항상 같음)
len 배열/슬라이스의 요소 개수
append(a, i) 슬라이스에 새로운 요소를 추가
copy(a, s) 슬라이스 s의 요소를 슬라이스 a에 복사
s = s[:cap(s)] 슬라이스의 길이를 용량만큼 증가시킴

배열생성
```
var a [5]int
b := [3]int{1, 2, 3}
c := [3]int[1,2] //초깃값지정하지않으면 0
d := [...]int{1,2,3,4,5}
e := [3][3]int{
    {1,2,3},
    {4,5,6}
}
```

슬라이스생성
```
var a []int
b := []int{}
c := []int{1,2,3}
d := [][]int{
    {1,2},
    {3,4,5},
}
```

순차조회
```
nums := []int{1,2,3,4,5,6,6}
for index, value := range nums{
    fmt.Println(index, value)
}
```

슬라이스 호출
s[n:m]
s[n:]
s[:m]
s[:]

## Map

```
map0 := map[string]int{}
map0["one"] = 1
map0["two"] = 2
map0["three"] = 3

map1 := map[string]int{
    "one":1,
    "two":2,
    "three":3
}

map2 := make(map[string]int, 3)
map2["one"] = 1
map2["two"] = 2
map2["three"] = 3
```

순차접근
```
for k, v := range map0 {
    fmt.Println(k, v)
}
```

`[]bypte []int32`은 string으로 변환해서 맵의 키로 사용가능

## 포인터와 참조


### 포인터 선언 할당

var p *int
i := 4
p = &i

### 이중포인터
var p *int
var pp **int

i := 5
p = &i
pp = &p

### 구조체 포인터

type rect struct{ w, h float64}
var s *rect = &rect{1,2}

### new로 포인터 생성

p := new(int)
*p = 1
fmt.Println(p) //주소
fmt.Println(*p) //1

r := new(rect)
r.w, r.h = 3, 4
fmt.Println(r)
fmt.Println(*r)

### 포인터 파라미터

go는 기본으로 값을 복사해서 전달
함수나 값 전달시 포인터 사용하면 메모리 절약

## go 우덜식 객체지향

상태를 표현하는 type과 동작을 표현하는 메서드를 분리해서 정의

메서드를 리시버로 정의하면 struct의 내부에 정의된다

interface정의방법 같은 메서드가 정의되어 있으면 같이 사용가능

### 정보은닉

소문자 private
대문자시작 public

### 인터페이스

type interfaceName interface{
    method1(param) retuntype
    method2(param) retuntype
}

익명인터페이스
func display(s interface {show()}){
    s.show()
}
고 언어의 덕타이핑이란 특성때문에 가능한 구조

빈 인터페이스
func display(s interface{}){
    fmt.Println(s)
}
func main(){
    display(1)
    display(2.5)
    display(&rect{3,4})
}

