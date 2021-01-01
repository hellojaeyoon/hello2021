## Greedy

---

Greedy 알고리즘은 `그때 그때의 상황에서 가장 좋은 것만 고르는 방법` 으로 문제를 푸는 알고리즘이다. 탐욕적으로 풀어야 되는 문제들은 매우 다양한 유형으로 있는데, 그 중에서 다익스트라 알고리즘이나 플로이드 위셜 처럼 미리 알고 있으면 편하게 풀 수 있는 문제들도 존재한다. 아래에 간단한 예시들을 살펴보자.

- ### 큰 수의 법칙

N개의 숫자들로 이루어진 배열이 있을때 그 배열의 숫자들을 M번 더하여(중복가능) 가장 큰 수를 만들고자 한다. 하지만 주어진 배열의 특정 인덱스에 해당하는 숫자는 최대 K번까지만 연속해서 더해질 수 있다고 할때, 주어진 N, M, K에 대하여 만들 수 있는 가장 큰 수를 구해보자.

Ex) N, M, K = 5, 8, 3 이고. 주어진 배열이 2, 4, 5, 4, 6 이라고 하면

6 + 6 + 6 + 5 + 6 + 6 + 6 + 6 = 46 이 가장 큰 수가 된다.

 N, M, K = 5, 7, 2 이고. 주어진 배열이 3, 4, 3, 4, 3 이라고 하면

4 + 4 + 4 + 4 + 4 + 4 + 4 = 28 이 가장 큰 수가 된다.

---

우선 나는 아래와 같이 코드를 짜보았다. 맹점은 아래와 같다.

- 가장 큰 수와 그 다음으로 큰 수, 이렇게 2가지의 숫자를 이용해서 더하면 우리가 원하는 가장 큰 수를 구할 수 있다.
- 가장 큰 수는 M - M // (K+1) 만큼, 그 다음으로 큰 수는 M // (K+1) 만큼 더해주면 된다.

```python
import time

start = time.time()
N, M, K = map(int, input().split())
Ls = list(map(int, input().split()))
# bigNum 이라는 배열에 가장 큰 수와 그 다음으로 큰 수를 저장한다.
bigNum = [0]*2
bigNum[0], bigNum[1] = Ls[0], Ls[1]
for i in range(N):
    if Ls[i] > bigNum[0]:
        bigNum[0], bigNum[1] = Ls[i], bigNum[0]
    elif Ls[i] > bigNum[1]:
        bigNum[1] = Ls[i]

ans = (M//(K+1))*bigNum[1] + (M - M//(K+1))*bigNum[0]

end = time.time()

print(ans)
print(f'Time: {end-start}')
'''
5 8 3
2 4 5 4 6
'''
```

```
5 8 3
2 4 5 4 6
46
Time: 1.081655502319336
```

---

그럼 문제에 대한 해설코드를 살펴보면,

```python
import time

start = time.time()

n, m, k = map(int, input().split())
data = list(map(int, input().split()))

data.sort()
first = data[n-1]
second = data[n-2]

result = 0

while True:
    for i in range(k):
        if m == 0:
            break
        result += first
        m -= 1
    if m == 0:
        break
    result += second
    m -= 1

end = time.time()

print(result)
print(f'time: {end-start}')
```

- 위와 같은 비효율적인 코드가 하나 주어지고(일일이 M번을 다 더하는 코드이다 )
- 아래와 같은 결과값을 가진다.

```
5 8 3
2 4 5 4 6
46
time: 2.2292652130126953
```

---

그리고 그 더하는 과정을 다시 간략하게 아래와 같이 고치는데, 이 때의 실행시간은 훨씬 짧게 나오는것을 볼 수 있다.

```python
import time

start = time.time()

n, m, k = map(int, input().split())
data = list(map(int, input().split()))

data.sort()
first = data[n-1]
second = data[n-2]

count = int(m / (k+1)) * k
count += m % (k+1)
result = 0
result += (count) * first
result += (m-count) * second
end = time.time()

print(result)
print(f'time: {end-start}')
```

- 아래와 같은 결과가 나온다

```
5 8 3
2 4 5 4 6
46
time: 1.2517662048339844
```

---

- 엄청나게 특별한 부분은 발견되지 않지만, 나는 배열에 있는 모든 원소를 하나하나 비교해가며 길이 2짜리 리스트에 가장 큰 숫자 2개를 저장했고, 해설에서는 그냥 전체 리스트를 sorting하고 가장 끝 2개의 숫자를 사용했다.
- 나는 배열의 길이 N에 비례하게 오래걸리는 연산, 즉 O(N)의 시간복잡도를 가지는 코드이고, 해설은 python에 내장된 sorting 알고리즘, O(N log N)의 시간복잡도를 가지는 코드이다. (물론 사실 N이 엄청 크진 않지만, 나는 가장 큰 두 수만 구하는것이기 때문에 더 짧다고 할 수 있다)
- 원래는 이런걸 전혀 깊게 생각하고 넘어가지 않았지만, 내 코드가 평소에 비효율적이라는 결론이 자주 나서, 꾸준하게 습관을 길러보고자 한다.

---

- ### 숫자 카드 게임

숫자카드게임은 여러 개의 숫자 카드 중에서, 아래와 같은 룰들을 지키며 카드를 한 장 뽑는 게임이다.

1. 숫자가 쓰여진 카드들이 N * M 형태로 놓여 있다.
2. 먼저 내가 뽑고자 하는 카드가 있는 행을 선택한다.
3. 그리고 그 행의 카드들 중 가장 숫자가 작은 카드를 뽑아야한다.

이 때 최대한 가장 높은 숫자를 뽑아보자.

입력은 아래와 같이 주어진다.

```
3 3
3 1 2
4 1 4
2 2 2

---> 원하는 답: 2
```



---

## MyCode

- 그냥 입력받은 행렬의 각 행에 대해 최솟값을 저장한 후
- 그 N개의 최솟값들중 최대값을 고르면 된다.

```python
N, M = map(int, input().split())
Ls = []
for i in range(N):
    hang = list(map(int, input().split()))
    Ls.append(min(hang))

print(max(Ls))

'''
3 3
3 1 2
4 1 4
2 2 2

2 4
7 3 1 8
3 3 3 4
'''
```

```
2

3
```

- 해설과 거의 유사하다

---

- ### 1 이 될 때까지

어떠한 수 N이 주어졌을때 N에 대해 N이 1이 될때까지 아래의 두 과정 중 하나를 반복적으로 수행하고자 한다.

1. N 에서 1을 뺀다
2. N을 K로 나눈다

여기서 2번은 N % K 이 0일때만 가능하다. 그럼 이 때 주어진 N에 대하여 1을 만들때까지 위 과정을 수행해야하는 최소 횟수를 구하여라.

N K 가 입력으로 주어진다. (N은 2이상 10만이하, K는 2이상 10만이하이다)

---

## MyCode

- 주어진 N, K에 대하여 0번이상의 과정들을 통해 N이 K의 배수가 되었을때, 무조건 2번 과정을 거쳐야한다. 그 시점에서 1번을 선택한다면 N이 N//K 가 될때까지 (N- N//K)번의 과정이 필요하다. K 가 2이상이므로 당연히 나누는게 옳은 선택이다.
- 즉 N에서 1씩 빼다가, K의 배수가 되었을때 K로 나누어주면 된다.
- N이 K보다 작아진다면, N-1만큼 1번을 실행해준다.

```python
N, K = map(int, input().split())
counter = 0
escape = False
if N < K:
    print(N-1)

else:
    while N >= K:
        while N % K != 0:
            N -= 1
            counter += 1
        N = N // K
        counter += 1

    print(counter + N-1)
```

```
25 3
6
```

- 해설코드와 크게 다를바가 없었다