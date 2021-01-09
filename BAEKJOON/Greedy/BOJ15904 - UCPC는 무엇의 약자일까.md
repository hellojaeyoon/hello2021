# BOJ15904 - UCPC는 무엇의 약자일까?

https://www.acmicpc.net/problem/15904

---

- 'UCPC'의 인덱스를 늘려가며 한 자 한 자 비교해, 인덱스값이 최종적으로 4에 도달하는지 마는지로 판별하였다

```python
import sys
In = sys.stdin.readline
def check(word):
    global index
    for c in word:
        if c == theS[index]:
            index += 1
            if index == 4:
                return

testS = list(map(str, In().split()))
#print(testS)
theS = 'UCPC'
index = 0
for word in testS:
    check(word)
    if index == 4:
        print('I love UCPC')
        break
if index < 4:
    print('I hate UCPC')
```

