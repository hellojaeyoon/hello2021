# TIL

- 진법 변환시에 일일이 하나씩 꺼내서 계산하지 말고, 아래와 같이 파이썬에 내장된 함수를 효율적으로 사용해주자.

`int(문자열, base)`

```python
num = '3212'
base = 5
answer = int(num, base)
print(answer)
```

```
432
```

---

- 파이썬에 있는 ljust, center, rjust와 같은 string method를 사용해서 코드를 깔끔하게 하자

```python
s = 'hellojaeyoon'
n = 20

ans = s.ljust(n) # 좌측 정렬
print(ans)
ans = s.center(n) # 가운데 정렬
print(ans)
ans = s.rjust(n) # 우측 정렬
print(ans)

ans = s.ljust(n, '7') # 좌측 정렬
print(ans)
ans = s.center(n, 's') # 가운데 정렬
print(ans)
ans = s.rjust(n, '1') # 우측 정렬
print(ans)
```

```
hellojaeyoon        
    hellojaeyoon    
        hellojaeyoon
hellojaeyoon77777777
sssshellojaeyoonssss
11111111hellojaeyoon
```

- 기본적으로 `ljust`, `center`, `rjust` 의 두번째 인자는 `''` 공백으로 생략되어 있지만, 길이1의 인자를 넣어주어, 정렬결과의 빈 칸에 넣어줄 수 있다.

- s.ljust(n, c) 는 정렬된 값을 return 하는 함수이기 때문에, 저장하거나 그대로 print를 해서 결과를 이용할 수 있다.

---

모든 대문자, 모든 소문자를 직접입력하지 않고 파이썬에서 정의해둔 상수를 이용할 수 있다.

```python
import string 

string.ascii_lowercase # 소문자 abcdefghijklmnopqrstuvwxyz
string.ascii_uppercase # 대문자 ABCDEFGHIJKLMNOPQRSTUVWXYZ
string.ascii_letters #대소문자 모두 abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
string.digits # 숫자 0123456789
```

- 솔직히 이 기능은 실제 코테에서 사용을 할지 잘 모르겠다. 조금 특수한 경우일것 같다.

---

## 2차원 리스트 뒤집기(매우 중요!)

이차원 배열 mylist가 주어졌을때, 행과 열이 뒤집힌 2차원 배열 `answer`를 나는 아래와 같이 만들었다. 하지만 python에 내장된 `zip` 함수를 이용해서 훨씬 간단히 할 수 있다.

```python
def solution(mylist):
    answer = [[] for _ in range(len(mylist[0]))]
    for i in range(len(mylist)):
        for j in range(len(mylist[0])):
            answer[j].append(mylist[i][j])
    return answer
```

## Enumerate

- `enumerate`는 리스트에서 값을 꺼내올 때, 인덱스를 붙여서 꺼내는 함수이다

```python
listA = ['hello','jaeyoon', 3]
print(list(enumerate(listA)))
for a in enumerate(listA):
    print(a)
print(enumerate(listA))
```

```
[(0, 'hello'), (1, 'jaeyoon'), (2, 3)]
(0, 'hello')
(1, 'jaeyoon')
(2, 3)
<enumerate object at 0x0000020D3FF44408>
```

- 아래와 같이 한 번에 딕셔너리를 만들때도 사용이 가능하다

```python
dictA = {i:j for i,j in enumerate('I am hellojaeyoon'.split())}
print(dictA)
```

```
{0: 'I', 1: 'am', 2: 'hellojaeyoon'}
```

---

## ZIP

`zip`은 여러개의 iterable에 대해 그 안의 요소들을 병렬적으로 꺼내온다.

zip(*iterables)는 각 iterables의 요소를 모으는 iterator을 만든다.

```python
A = [1, 2, 3, 4, 5]
B = 'My name is hello jaeyoon'

for i in zip(A,B):
    print(i)
    
B = ['My', 'name']
for i in zip(A,B):
    print(i)
```

```
(1, 'M')
(2, 'y')
(3, ' ')
(4, 'n')
(5, 'a')
(1, 'My')
(2, 'name')
```

- 위와 같이 가장 짧은 길이의 iterable에 대해서 꺼내오고 멈추게 된다.

그렇다면 원래 우리가 하려고 했던 2차원 배열 뒤집기는 아래와 같이 할 수 있다.

```python
mylist = [ [1,2,3], [4,5,6], [7,8,9] ]
print(*mylist)
print(list(map(list,zip(*mylist))))
```

```
[1, 2, 3] [4, 5, 6] [7, 8, 9]
[[1, 4, 7], [2, 5, 8], [3, 6, 9]]
```

---

## itertools.product

- 솔직히 이건 코테에서 사용하지 못할것 같지만 일단 익혀두었다

```python
import itertools

iterable1 = 'ABCD'
iterable2 = 'xy'
iterable3 = '1234'
for a in itertools.product(iterable1, iterable2, iterable3):
    print(a)
```

```
('A', 'x', '1')
('A', 'x', '2')
('A', 'x', '3')
('A', 'x', '4')
('A', 'y', '1')
('A', 'y', '2')
('A', 'y', '3')
('A', 'y', '4')
('B', 'x', '1')
('B', 'x', '2')
('B', 'x', '3')
('B', 'x', '4')
('B', 'y', '1')
('B', 'y', '2')
('B', 'y', '3')
('B', 'y', '4')
('C', 'x', '1')
('C', 'x', '2')
('C', 'x', '3')
('C', 'x', '4')
('C', 'y', '1')
('C', 'y', '2')
('C', 'y', '3')
('C', 'y', '4')
('D', 'x', '1')
('D', 'x', '2')
('D', 'x', '3')
('D', 'x', '4')
('D', 'y', '1')
('D', 'y', '2')
('D', 'y', '3')
('D', 'y', '4')
```

---

### 2차원 리스트 -> 1차원 리스트

나는 하나하나 append로 더해주어서 정말 비효율적이었다. 아래 방법이 보통 사람들이 쓰는 방법이라고 한다.

```python
my_list = [[1, 2], [3, 4], [5, 6]]
answer = []
for i in my_list:
    answer += i
```

그보다 효율적이게 많은 방법들이 있는데 그 중 나는 아래와 같은 방법들에 집중했다.

```python
my_list = [[1, 2], [3, 4], [5, 6]]
# 방법 1 - sum 함수
answer = sum(my_list, [])

# 방법 2 - itertools.chain
import itertools
list(itertools.chain.from_iterable(my_list))

# 방법 3 - itertools와 unpacking
import itertools
list(itertools.chain(*my_list))

# 방법4 - list comprehension 이용
[element for array in my_list for element in array]
```

- 여기서 sum 함수의 두 번째 인자에 0이 들어오는데, my_list안의 list들을 그대로 더해주려면, 숫자 0으로는 error가 발생한다. 따라서 sum을 start하는 인자(즉 sum()의 두 번째 인자에 빈 배열을 넣어준다)

---

#### itertools.permutations(iterables, n)

- n개의 원소를 가진 모든 순열을 tuple들 형태로 return한다.
- 2번째 인자를 생략하면 iterable길이의 순열들을 return 한다.
- 문제를 풀다보면 순열을 이용해야하는 경우가 많은데, 이걸 이렇게 python 내장함수로 그냥 사용해도 되는지 의문이긴하다.

---

## List Comprehension (!)

list를 입력받아, 리스트의 원소들중에서 짝수인것들에 대해, 그 원소의 제곱값들을 모아놓은 리스트를 반환해보자.

```python
mylist = [3, 2, 6, 7]
answer = []
for i in mylist:
    if i%2 == 0:
        answer.append(i**2) # 들여쓰기를 두 번 함
```

나의 코드도 위와 거의 똑같았는데, 이걸 list comprehension을 이용해서 한 번에 쓸 수 있다

```python
mylist = [3, 2, 6, 7]
answer = [ i**2 for i in mylist if i %2 == 0]
```

- 위와같이 짜는거에 익숙해지는게 좋아보인다.

---

### 무한대, -무한대

- 다익스트라에서 몇 번 쓴적이 있는데, 평소에는 잘 안썼다 난.

```python
min_val = float('inf')
max_val = float('-inf')
```

---







