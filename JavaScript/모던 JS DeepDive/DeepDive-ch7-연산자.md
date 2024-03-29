## 7장

연산자는 하나 이상의 표현식으로 산술, 할당, 비교, 논리, 타입, 지수 연산 등을 수행해 하나의 값을 만듬

```javascript
// 산술 연산자
5 * 4 // 20

// 문자열 연결 연산자
'My name is' + 'Lee'

// 할당 연산자
color = 'red'

// 비교 연산자
3 > 5 // false

// 논리 연산자
ture && false // false

// 타입 연산자
typeof 'Hi' // String
```

### 1. 산술 연산자
수학적 계산
> 이항 산술 연산자: *, -, +, /, %  
단행 산술 연산자: ++, --, +, -

### 2. 문자열 연결 연산자
+로 문자열 연결

```javascript
1 + ture // 2
1 + fasle // 1
1 + null // 0
```

### 3. 할당 연산자
=, +=, -=, *=, /=, %=  
### 4. 비교 연산자
if 또는 for 문에서 주로 사용

- ==(동등), ===(일치), !=(불동등), !==(불일치)

> 동등 비교와 일치 비교
동등 비교: 조, 우항의 피연산자 비교 시 타입 변환을 통해 타입을 일치시킨 후 값 비교
일치 비교: 타입도 같고 값도 같아야 ture 반환  

### 5.삼항 조건 연산자

```
'' 조건식 ? 조건식이 true일 때 반환할 값 : 조건식이 false일 때 반환할 값
```
-> 삼항 조건 연산자 표현식은 값으로 표현할 수 있는 표현식인 문이다.

### 6. 논리 연산자
||(or), &&(AND), !(NOT)

### 7. typeof 연산자
- 'typeof null' 시 object 반환(JS의 버그)
-> thypeof 대신 일치 연산자 사용 


### 8. 지수 연산자
** 사용

### 9. 그 외의 연산자

> **?.**: 옵셔널 체이닝 연산자
**??**: null 병합 연산자  
**delete**: 프로퍼티 삭제  
**new**: 생성자 함수 호출 시 사용해 인스턴스 호출  
**instanceof**: 좌변의 객체가 우변의 생성자 함수와 연결된 인스턴스인지 판별  
**in**: 프로퍼티 확인

<br>

### 연산자 우선 순위
> 1. ()
> 2. new(매개변수 존재)  
> 3. .[], (), ?.  
> 4. new(매개변수 미존재)
> 5. X++, X--
> 6. !X, +X, -X, ++X, --X, typeof, delete  
> 7. **
> 8. *, /, %
> 9. <, =, >
> 10. in, instanceof
> 11. ==, !=, ===, !==
> 12. ??
> 13. &&
> 14. ||
> 15. ? ... : ...
> 16. 할당 연산자, .


