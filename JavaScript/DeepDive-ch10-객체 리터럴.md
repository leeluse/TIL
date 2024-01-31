## 객체 리터럴

- JS는 객체 기반의 프로그래밍 언어, JS를 구성하는 모든 것이 객체
- 원시 타입의 값, 즉 원시값은 변경 불가능한 겂이지만 객체타입, 즉 객체는 변경 가능한 값이다.  
- 객체는 0개 이상의 프로퍼티로 구성, 프로퍼티는 키와 값으로 구성되어 있다.

``` js
var person = {
  name: 'Lee', // 키: name, 값: Lee
  age: '20'  // 키: age, 값: 20
};

var Counter = {
  num: 0,
  increase: function() {
    this.num++;
  }
};
```

> 프로퍼티: 객체의 상태를 나타내는 값  
메서드: 프로퍼티를 참조하고 조작할 수 있는 동작

<br>

#### 객체와 함수  
- JS에서 객체와 함수는 밀접함  
함수로 객체를 생성하기도 하고 함수 자체가 객체기도 하다.  
- C++이나 자바 같은 객체 지향 언어는 클래스 정의 후 필요 시점에 new 연산자와 함께 생성자를 호출하여 인스턴스를 생성하는 방식  
- JS는 프로토타입 기반 객체 지향 언어로 다양힌 객체 생성 방법 지원
  - 객체 리터럴
  - Object 생성자 함수
  - object.create 메서드
  - 클래스(ES6) 문법


####  객체 리터럴 방식  
중괄호 ({...}) 내에 0개 이상의 프로퍼티 정의
```js
var person {
  name: 'Lee',
  sayHello: function() {
    console.log('Hello! my name is' + ${this.name});
  }
};
``` 
#### 프로퍼티  
객체는 프로퍼티의 집합이며 키와 값으로 구성되어 있다  
> 식별자 네이밍 규칙을 준수하지 않는 프로퍼티 키는 따옴표 사용  
프로퍼티 키 동적 생성도 가능

``` js
var obj = {};
var key = 'hello';

obj[key] = 'world!'
console.log(obj); // {'hello', 'world!'}
```

#### 메서드
JS에서 사용할 수 있는 모든 값은 프로퍼티 값으로 사용할 수 이ㅆ다.  
JS에서 함수는 객체 -> 함수는 값으로 취급 가능 -> **프로퍼티 값으로 사용 가능**  
프로퍼티 값이 함수일 경우 구분하기 위해 이를 **메서드**라고 부른다  

``` js
var circle = {
  radius: {
    getDiameter: function () {
      return 2 * this.radius;
    }
    console.log(circle.getDiameter()); // 10
  }
} 
```

#### 프로퍼티 접근
> 마침표 프로퍼티에 접근(.) 연산자 사용 -> **마침표 표기법**  
대괄호 프로퍼티에 접근([]) dustkswk tkdyd -> **대괄호 표기법**

``` js
var person = {
  name: 'Lee'
}
// 마침표 프로퍼티 접근
console.log(person.name);
// 대괄호 프로퍼티 접근
console.log(person['name']); // 꼭 따옴표 사용!
```


프로퍼티 동적 생성
``` js
person.name = 'Kim'
```


프로퍼티 삭제
``` js
delete person.name;
```