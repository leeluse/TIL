## 타입 변환과 단축 평가


### 타입 변환?  
개발자가 의도적으로 값의 타입을 변환 시키는 것   
-> **명시적 타입 변환 또는 타입 캐스팅**  
개발자의 의도와 상관없이 도중 JS 엔진에 의해 암묵적으로 타입 변환  
-> **암묵적 타입 변환 또는 타입 강제 변환**  


### 암묵적 타입 변환
1. 문자열 타입 변환: + 연산자 사용 중 하나 이상의 문자열 포함 시 암묵적 문자열 타입으로 변환
2. 숫자 타입 변환: 산술 연산자를 이용 
3. 불리언 타입 변환: 논리적 참/거짓으로 평가되는 표현식 사용 -> Truthy or Falsy로 구분

<br>

### 명시적 타입 변환  
표준 빌트인 생성자 함수(String, Number, Boolean)를 new 연산자 없이 호출하는 방법과 빌트인 메서드를 사용하는 방법 그리고 암묵적 타입 변환 이용

#### 문자열 타입 변환
1. String 생성자 함수를 new 연산자 없이 호출하는 방법
```String(1) // '1'```
2. object, prototype, toString 메서드를 사용하는 방법 
```(1).toString(); // '1' ```   
3. 문자열 연결 연산자를 이용하는 방법
```1 + '' // '1' ```

#### 숫자 타입 변환
1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
```Number('5') // 5```
2. parseInt, parseFloat 함수를 사용하는 방법 
```parseInt('5') // 5 ```   
3. '*' 산술 연산자를 이용하는 방법
```'0' * 1 -> 0, true * 1 -> 1 ```

#### Boolean 타입 변환
1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
```Boolean('X') -> true```
2. ! 부정 논리 연산자를 두 번 사용하는 방법 ```!!'X' -> true```

<br>


### 단축 평가
|| 또는 && 또는 연산자 표현식의 결과가 불리언이 아닐 수도 있음
``` javascript
'cat' && 'dog' //'dog'
'cat' || 'dog' //'cat'
```
표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가과정을 생략하는 것

<br>

- 옵셔널 체이닝 연산자  
>?.는 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참고를 이어간다.
``` javascript
var elem = null;
var value = elem?.value;

console.log(value) // null
```

- null 변합 연산자  
>??는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다  
``` javascript
var foo = null ?? 'default string';
console.log(foo); // default string
```



