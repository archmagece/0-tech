# 고루틴

고언어의 차별점 중 하나.

코틀린이나 clojure에서도 고루틴과 비슷한게 있는데

어디가 원조일까..

주의점1. 고루틴은 메인함수가 종료될 때 강제 종료된다. channel을 만들어 고루틴의 종료를 기다려줘야한다.
await비슷한 느낌

## 채널 선언
```
방법1
var ch chan string
ch = make(chan string)
방법2
ch := make(chan string)

go g0_routione_func(ch)
<-ch
```

## 채널방향
```
chan<- string //송신전용채널
<-chan string //수신전용채널
```

## 버퍼드 채널

버퍼드 채널은 비동기 방식으로 동작, 채널이 꽉 찰 때까지 채널로 메세지를 계속 전송. 채널이 빌 때까지 메시지를 계속 수신
```
ch := maek(chan int, 100)
```

버퍼가 가득차면 입력 고루틴은 대기

## 채널닫기

close(ch)S

v, ok := <- ch
ok false이면 채널에 더 이상 값이 없음
for i := range c
채널 c가 닫힐 때까지 반복하여 채널로부터 수신


## select

하나의 고루틴이 여러개의 고루틴과 통신할 대

```
select {
    case <- x:
        x, y = y, x+y
    case <- quit:
        fmt.Println("quit")
        return
    default:
        fmt.Println("    ")
        tiem.Sleep(10)
}
```

## 저수준 제어

sync 패키지에

mutex로 공유 메모리를 제어할 수 있는 기능

sync/atomic 패키지에 원자성을 보장할 수 있는 연산(add, compare, swap 등)

### lock
```
func (m *Mutex) Lock()
func (m *Mutex) Unlock()

runtime.GOMAXPROCS()
runtime.NumCPU()

func (rw *RWMutex) Lock() :쓰기잠금
func (rw *RWMutex) Unlock()
func (rw *RWMutex) RLock() : 읽기잠금
func (rw *RWMutex) RUnlock()
```

### sync.Once
`sync.Once` 구조체는 다음 메서드를 제공

`func (o *Once) Do(f func())`

static 변수처럼 한번만 실행되는 함수.

### sync.WaitGroup

모든 고루틴이 종료될 때 까지 대기해야될 때 사용

```
func (wg *WaitGroup) Add(delta int): wait group에 대기중인 고루틴 개수 추가
func (wg *WaitGroup) Done(): 대기중인 고루틴의 수행이 종료되는 것을 알려줌
func (wg *WaitGroup) Wait(): 모든 고루틴이 종료될 때까지 대기
```

### sync/atomic패키지 - Atomic 원자성 보장 연산

AddT 특정 포인터 변수에 값을 추가
CompareAndSwapT 특정 포인터 변수의 값을 주어진 값과 비교하여 같으면 새로운 값으로 대체
LoadT 특정 포인터 변수의 값을 가져옴
StoreT 특정 포인터 변수에 값을 저장함
SwapT 특정 포인터 변수에 새로운 값을 저장하고 이전 값을 가져옴

### 파이프라인

`find src | grep .go$ | xargs wx -l`

io.Pipe()를 사용하면 유닉스 스타일로 파이프라인을 생성할 수 있다.

그런데 그것보다 고루틴을 여러개 파이프라인으로 연결해서 메시지플로우를 만들어버린다.

### 맵리듀스

....

