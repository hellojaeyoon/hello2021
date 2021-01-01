# Input Vs Sys.stdin.readline

python

## input() vs sys.stdin.readline()

알고리즘 문제를 단계별로 푸는 극 초반부에, input()으로 문제를 풀면 시간초과가 나지만 sys.stdin.readline()을 이용하면 문제 없이 넘어가는 상황이 생겼다. 나의 얕은 지식을 조금이라도 늘릴겸 알아보았다.

<출처>

https://www.geeksforgeeks.org/difference-between-input-and-sys-stdin-readline/

https://en.wikipedia.org/wiki/Standard_streams#:~:text=provide%20equivalent%20functionality.-,Standard%20input%20(stdin),all%20programs%20require%20stream%20input.



---

#### Input()

- `input()`은 사용자의 입력값을 받아 그 값을 evaluate한다. 즉 Python이 자동으로 입력된 값이 string인지 number인지 list인지 파악하는 단계를 거친다. 만약 그 값이 옳지 않다면 `syntax error` 나 `exception`이 발생하게 된다.
- `input()` 함수가 실행되면 사용자의 입력이 있기전까지 program flow가 멈춘다.
- 사용자가 어떤 입력을 input()에 하던 input()함수는 입력값을 string으로 변환하다. 사용자가 정수를 입력했더라도 그 값을 string으로 변환하기 때문에 정수로 사용하려면 다시 변환해주어야한다.

#### Sys.stdin.readline()

- `Stdin` 은 `Standard input`의 줄임말로 프로그램이 입력된 데이터를 읽는 스트림이다.

```
여기서 Standard Stream이란 프로그램 실행을 시작할때 컴퓨터 프로그램과 그 환경 사이의 상호연결된 입력/출력(I/O) 통신채널을 일컷는다. 입력/출력 연결은 다음과 같이 standard input (stdin), standard output (stdout), standard error (stderr) 3가지가 있다.
```

- `input()`과는 달리 사용자가 입력한 escape character도 읽는다.
- 그리고 sys.stdin.readline(k) 와 같이 한 번에 읽을 character의 갯수를 제한하는 파라미터를 제공한다(k)

input()과 readline()의 차이점

- input()은 선택적으로 실행되는 interpreter가 있다면 보여주는 prompt parameter를 가지고 있다. 이것은 prompt가 비어 있는 경우에도 overhead를 초래한다.

- input()은 개행 문자를 제거해준다. readline()은 strip()을 추가해줘야 한다.

- input()은 더이상 입력을 하지 않을 때 EOFError를 증가시킨다.
  하지만 readline()은 EOF에서 빈 문자열을 반환한다.

---

즉 수많은 행의 입력값이 존재할때, 매 번 evaluate를 거치는 input() 이 readline() 보다 훨씬 더 느리다.