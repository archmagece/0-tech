# golnag 문법

## 문법

### 반복문
while 없음 for

1. for i := 0; i< 10; i++{}
2. for i < 10 {}
3. for {}

### 논리
if-else 없음
switch case

```
switch {
case i == 1:
  fmt.println()
case i > 1:
  fmt println()
```

### 모호한거
```c
i = i++
i = ++i
```
가능한것
```
i += 1
i++
num = i
```

### 세미콜론
생략가능

### 주석
```
// 주석내용
/* 주석내용 */
```

### 변수

```
var 변수명 타입
var a int
var (
  name string
  age int
)
```

타입생략
```
var c = true
var size = uint16(1024)
```