# BOJ11399 - ATM

https://www.acmicpc.net/problem/11399

---

각 사람이 돈을 인출하는데에 걸리는 시간을 기준으로 총 필요한 시간의 합을 계산해보자.

첫번째 사람이 돈을뽑는데에 걸리는 시간을 t_1 이라고 한다면, 첫번째 사람을 포함해서 모두 N명의 사람이 t_1만큼 기다리게 된다.

따라서 우리가 구하는 답인 각 사람이 돈을 인출하는데 필요한 시간의 총합은

t_1 * N + t_2 * (N-1) + ... + t_N * 1이 된다.

따라서 각 사람이 인출하는데에 걸리는 시간을 내림차순으로 정렬해야 우리가 원하는 최솟값을 구할 수 있다.

```python
N = int(input())
time = list(map(int, input().split()))
time.sort()
ans = 0
for t in range(N):
    ans += (N-t)*time[t]
print(ans)
```

