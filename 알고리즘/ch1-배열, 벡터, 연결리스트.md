### 배열 Array
- 삽입/삭제: O(N)  
- 탐색: O(1)  
- C++에서는 size 변경 불가  
- Python은 리스트 사용

<br>

배열을 생성하면 메모리에 연속된 공간을 생성하게 됨


#### 임의 접근(random access)
``` python
arr = [10, 11, 12, 13]
arr[2] = 5
```
arr[2] -> arr + 2 * 4byte = 메모리 주소값  
arr에서 2 인덱스의 값을 지우고 그 공간에 5를 넣어 주는 방식

<br>

_삽입/삭제가 O(N)인 이유?_

메모리에 공간을 추가/제거하기 위해 N 만큼의 이동이 필요  
~> 삽입/삭제를 한 번 할 때마다 N의 위치에 넣기 위해 N번 만큼의 이동이 발생


**탐색을 할 시에는 배열이 유리**

<br>

### 벡터 Vector
- 삽입/삭제: O(N)  
- 탐색: O(1)  
- 동적 배열 (Size 변경 가능)

<br>


**동적 배열이라는 특징 외에 배열과 동일**

<br>

_파이썬의 튜플_  

``` python
v = []
v.append((123, 456))
v = []
v.append((789, 987))
print("size": len(v))
for p in v:
  print(p) // 2
```


> 123, 456 그리고 789, 987 이렇게 두 개의 요소를 지니고 있기에 print는 2를 출력

<br>

### 연결 리스트 Linked List
- 삽입/삭제: O(1)  
- 탐색: O(N)  
- Python에서는 직접 구현해야 함

연결 리스트의 경우, 노드가 메모리 주소값이 랜덤하게 위치하고 있다.



#### 노드의 구성  
[노드가 저장하려는 값 | 다음 노드 주소 값]

- 탐색  
임의 접근을 제공하지 않기에 특정 노드 값을 찾기 위해서는 루트 노드에서 시작해서 탐색해야 한다.  
- 삽입/삭제  
노드의 값을 담고 있는 것을 생성하여 연결만 해 주면 된다.  
연결 관계를 이어 주거나 삭제하는 것이 다기에 O(1)이다.
