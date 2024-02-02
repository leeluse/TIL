### 스택 Stack
- 삽입/삭제: O(1)

<br>

#### LIFO와 FILO  
>**LIFO**: Last In First Out  
**FILO**: First In Last Out


``` python
s = []
s.append(123)  
s.append(456)  
s.append(789)  
print("Size: ", len(s))
while len(s) > 0:
  print(s[-1])
  s.pop(-1)
```


```S [ 123 | 456 | 789 ]```
<br>  
_파이썬에서 -1를 사용할 시 역순으로 시작_  
pop으로 제거되는 순서: 789, 456, 123

### 큐 Queue
- 삽입/삭제: O(1)

<br>

#### FIFO와 LILO
>**FIFO**: Fiist In First Out  
**LILO**: Last In Last Out

``` python
from collections import deque

q = deque()
q.append(123)
q.append(456)
q.append(789)
q.appendleft(45) // 앞으로 값을 넣음  
print("size:", len(q))
while len(q)>0:
  print(q.popleft())
```
_deque을 사용하는 이유_  
: 양방향 IN/OUT 가능
<br>


```S [ 123 | 456 | 789 ]```
<br>  
