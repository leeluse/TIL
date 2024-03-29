## 제어문

조건에 따라 코드 블록을 실행하거나, 반복 실행할 때 사용

### 1. 블록문  
0개 이상의 문을 중괄호로 묶은 것  
코드 블록 또는 블록이라고 부르기도 함 -> JS의 실행 단위
-  세미콜론 = 종결문을 의미 하기에 블록문의 끝에는 세미콜론을 붙이지 않는다  

```javascript
// 블록문
var foo = 10;
```
```javascript
// 제어문
var X = 1;
if (X < 10) {
  X++;
}
```

```javascript
// 함수 선언문
fucntion sum(a, b) {
  return a + b;
}
```


### 2. 조건문

#### 1. if... else 문  
논리적 참 또는 거짓에 따라 실행할 블록 코드 결정  
삼항 조건 연산자로 변경 가능

```javascript
for(선언문 or 할당문; 조건식; 증감식) {
  조건식이 참인 경우 반복 실행될 문;
}
```
```javascript
for (;;) {...} // for 무한 루프문
```



<br>

#### 2. while문  
주어진 식이 참일 경우 게속 반복 실행

> **for** : 횟수가 명확할 때 사용
> **while** : 횟수가 불명확할 때 사용

<br>

#### 3. do... while문  
코드 블록을 먼저 실행하고 조건식 평가  
* 코드 블록이 무조건 한 번 실행된다

<br>

#### 4. break문  
반복문, switch문을 탈출  
- 레이블 문: 식별자가 붙은 문   
ex) ```foo: console.log('foo');```


#### 5. continue문
반복문의 코드 블록 실행을 현 시점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동 시킨다.  
-> 반복문을 탈출하지 않음