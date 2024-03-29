## 데이터 타입

데이터 타입 = 값의 종류  
JavaScript의 모든 값은 데이터 타입을 가진다  
JS ES6 문법에는 7개의 데이터 타입이 존재한다

> 원시: 숫자, 문자열, 불리언 Undefined, null, 심벌 타입  
객체: 객체, 배열, 함수 등

<br>

### undefined와 null의 차이점?  
**undefined**: var 키워드로 선언된 변수에 암묵적으로 할당되는 값  
**null**: 값이 없다는 것을 의도적으로 명시해 둔 것

<br>

### 1. 숫자 타입
다른 언어들과 다르게 하나의 숫자 타입을 제공  
ECMAScript 기준 -> 모든 숫자 타입을 <u>실수</u>로 처리


_세 가지 특별한 값 표현_
- infinity: 양의 무한대
- -infinity: 음의 무한대
- NaN: 산술 연산 불가(JS는 대소문자를 구분하기에 주의)

<br>

### 2. 문자열 타입
- 텍스트 데이터를 나타내는 데 사용
- '', "", `` 사용


<br>

### 3. 템플릿 리터럴
- ES6에서 새롭게 도입
- 멀티라인 문자열, 표현식 삽입 등 편리한 문자열 처리
- ``(백틱) 사용


### 4. 불리언 타입
논리적 참, 거짓을 나타내는 True, False 사용

**null**
1. 변수에 값이 없다는 것을 의도적으로 명시
2. 변수가 이전엥 참조하던 값을 더 이상 참조하지 않겠다는 의미  
      => 참조를 명시적으로 제거
3. 함수가 유효한 값을 변환할 수 없는 경우에도 null 반환


<br>

### 5. Undefined 타입
undefined 타입의 값은 undefined가 유일   
var 키워드로 선언한 변수는 암묵적으로 undefined로 초기화된다
- 선언과 정의  
-> <u>'실제로 메모리 주소를 할당하는가?'</u>
> 선언: 단순히 컴파일러에게 식별자의 존재만을 알리는 것  
정의: 실제로 컴파일러가 변수를 생성하여 메모리 주소를 연결하는 것

<br>

### 6. 심벌 타입
ES6에서 추가된 타입이며 변경 불가능한 원시 타입이다
다른 값과 중복되지 않는 유일무이한 값

심벌 이외의 값: 리터럴을 통해 생성  
심벌: symbol이 함수를 호출해 생성

<br>

### 7. 객체 타입
원시 타입과 객체 타입으로 구분되는 이유: 둘은 근본적으로 다름  
-> 자바스크립트를 이루는 거의 모든 것이 객체


#### 데이터 타입이 필요성
- 데이터 타입에 의한 메모리 공간의 확보와 참조
- 변수에 할당되는 데이터 값에 따라 메모리 공간의 크기를 결정한다

<br>

> 1. 값 저장 시 확보해야 하는 메모리 크기를 결정하기 위해
> 2. 값을 참조할 때 한 번에 읽어들여야 할 메모리 크기를 결정하기 위해
> 3. 메모리에서 읽어들인 2진수를 어떻게 해석할지 결정하기 위해 

<br>

### 동적 타이핑
C나 자바: 정적 타입 언어는 변수 선언 시 할당할 수 있는 값의 종류
즉, 데이터 타입을 사전에 선언 ->  **명시적 타입 선언** 
JS: 변수 선언 시 타입을 지정하지 않는다  
var, let, const 키워드를 사용해 변수를 선언할 뿐이다  
- typeofL 변수에 할당된 데이터 타입을 결정 -> 타입 추론  
- 재할당에 의한 변수의 타입은 언제든 동적으로 변경 가능 -> 동적 타이핑

<br>


## 용어 정리
- 심벌 테이블: 컴파일러 또는 인터프리터는 심벌 테이블이라고 부르는 자료 구조를 통해 식별자를 키로 바인딘된 값의 메모리 주소, 데이터 타입, 스코프 등을 관리
- 정적 타입 언어: 변수에 선언한 타입에 맞는 값만 할당 가능



