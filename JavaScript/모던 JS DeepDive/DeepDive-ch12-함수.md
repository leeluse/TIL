## 함수

>함수란?  
함수는 JS의 핵심 개념인 스코프, 실행 컨텍스트, 클로저, 생성자 함수에 의한 객체 생성, 메서드, this, 프로토타입, 모듈화과 관련 있다 

<br> 

수학의 함수: 입력과 출력을 내보내는 일련의 과정  
f(x, y) = x + y에 값을 전달하면 값을 계산한 결과가 출력

``` js
// 함수 정의
function add(x, y) {
  return x + y;
}
// 함수 호출
add(3, 4)
```
> 함수 이름: add  
매개변수: x, y   
반환 값: x + y  
인수: 3, 4

매개변수로 인수를 전달 -> 함수 호출  
#### 함수를 사용하는 이유?
함수는 코드의 재사용 측면에서 유용 -> 유지보수의 편이성 & 코드의 신뢰성 & 코드의 가독성 향상  

### 함수 리터럴  
JS의 함수는 객체 타입의 값  
숫자 값을 리터럴로 생성하고 객체를 객체 리터럴로 생성하 듯, 함수도 함수 리터럴로 생성 가능  
- 함수 리터럴: function 키워드, 함수 이름, 매개변수 목록, 함수 몸체  

``` js
// 변수에 함수 리터럴 할당
var f = function add(x, y) {
  return x + y;
}
```
즉, 함수는 **객체**다

<br>

> 함수 선언문  
``` js
function add(x, y) {
  return x + y;
}
```  
- 함수 이름 생략 불가능  
- 함수 선언문은 표현식이 아닌 문이다 -> console.log 출력 시 undefined 출력

<br>
<br>

> 함수 표현식  
``` js
var addFunction = function add(x, y) {
  return x + y;
};
```
- 함수 이름으로 호출하는 것이 아닌 함수 객체를 가리키는 식별자로 호출  
- console.log(add(x, y)) X  
console.log(addFunction(x, y)) O

<br>
<br>

> Function 생성자 함수  
``` js
var add = new Function('x', 'y', 'return x + y');
```

<br>
<br>

> 화살표 함수  
``` js
var add = (x, y) => x + y;
```

<br>

### 함수 생성 시점과 호이스팅
``` js
// 함수 참조
console.dir(add) // f add(x, y)
console.dir(sub) // undefined

// 함수 호출
console.log(add(2, 5)); // 7
console.log(sub(2, 5)); // TypeError: sub is not a fuction

// 함수 선언문
function add(x, y){
  return x + y;
}

// 함수 표현식
var sub = function (x, y) {
  return x + y;
};
```

함수 선언문으로 정의한 함수 -> 선언문 이전에 호출 가능  
함수 표현식으로 정의한 함수 -> 표현식 이전에 호출 불가능  

<br>

> **함수 호이스팅과 변수 호이스팅의 차이**  
**var 키워드를 사용한 변수 선언문**과 **함수 선언문**은 런타임 이전에 JS 엔진에 의해 먼저 실행되어 식별자를 생성  
- var 키워드로 선언된 변수는 undefined로 초기화  
- 변수 선언문을 통해 암묵적 생성된 식별자는 함수 객체로 초기화



함수 표현식? -> 변수에 할당되는 값이 함수 리터럴인 문  

변수 할당문의 값은 할당문이 실행되는 시점, 런타임에 평가되므로 함수 표현식의 함수 리터럴도 실행되는 시점에 평가되어 함수 객체가 된다


<br>

### Function 생성자 함수  
- JS가 기본 제공하는 빌트인 함수  
- Function 생성자 함수에 매개변수 모록과 함수 몸체를 전달하면서 new 연산자와 함께 함수 객체를 생성해서 반환
- Function 생성자 함수를 통해 생성하는 방식은 일반적이지 않고 바람직하지도 않음  
- Function 생성자 함수로 생성한 함수는 클로저를 생성하지 않는 등 다르게 동작함  

<br>

### 화살표 함수  
ES6에서 도입된 화살표 함수는 function 키워드 대신 화살표 => 를 사용해 간략하게 함수 선언 가능  

``` js
// 화살표 함수
const add = (x, y) => x + y;
console.log(add(2, 5)); // 7
```

<br>
<br>



### 함수 호출
매개변수와 인수
- 함수를 실행하기 위해 필요한 값을 함수 외부 -> 내부로 전달 시 사용
- 초과된 인수는 버려지지 않고 arguments 객체의 프로퍼티에 보관  
- 매개변수의 최대 개수는 적을수록 좋음  
  _이상적인 함수는 한 가지 일만 해야 하며 가급적 작게 만드는 것이 좋다_

<br>

### 반환문
- return 키워드로 값을 반환한다
- 함수 호출은 표현식이다
- 반환문의 두 가지 역할  
  1. 함수 실행을 중단하고 함수 몸체를 빠져나간다.
  2. return 키워드 뒤에 오는 표현식을 평가해 반환한다.

<br>

### 참조에 의한 전달과 외부 상태의 변경
```js
// 매개변수 p는 원시 값을 전달 받고, 매개변수 o는 객체를 전달 받는다.
function changeVar(p, o) {
  p += 100;
  o.name = 'Kim';
}

var num = 100;
var person = { name: 'Lee' };
// 원시 값은 자체가 복사되어 전달되고, 객체는 참조 값이 복사되어 전달된다.
changeVal(num, person);

// 원시 값은 원본이 훼손되지 않는다.
console.log(num);
// 객체는 원본이 훼손된다.
console.log(person);
```


### 다양한 형태의 함수
#### 즉시 실행 함수
``` js
(function () {
  var a = 3;
  var b = 2;
  return a + b;
}());
```
- 즉시 실행 함수도 값 반환과 인수 전달 가능

-  기명 즉시 실행 함수
``` js
(function foo() {
  var a = 3;
  var b = 2;
  return a + b;
}());
```

<br>

#### 재귀 함수
- 함수가 자기 자신을 호출하는 것  
- 재귀 함수는 반복되는 처리를 위해 사용

```js
function countdown(n) {
  for (var i = n; i >= 0; i--) console.log(i);
}
countdown(10);
```
#### 중첩 함수
- 함수 내부에 정의된 함수를 중첩 또는 내부 함수라고 부름  
- 일반적으로 중첩 함수는 자신을 포함하는 외부 함수를 돕는 헬퍼 함수 역할을 한다

```js
function outer() {
  var x = 1;
  function inner() {
    var y = 2;

    console.log(x + y); // 3
  }
  inner();
}
outer();
```
#### 콜백 함수
- 함수의 매개변수를 통해 다름 함수의 내부로 전달되는 함수  
  매개 변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수를 고차함수 라고 한다.


``` js
function repeat(n, f) {
  for (var i = 0; i < n; i++) {
    f(i);
  }
}

var logAll = function (i) {
  console.log(i);
};
// 반복 수행할 횟수와 함수를 인수로 전달
repeat(5, logAll); 0 1 2 3 4

var logOdds = function (i) {
  if (i % 2) console.log(i);
};

// 반복 수행할 횟수와 함수를 인수로 전달
repeat(5, logOdds); // 1 3
```

<br>

## 용어 정리
- 호이스팅: 함수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 JS 특징을 함수 호이스팅이라고 한다.

- 생성자 함수: 객체를 생성하는 함수


