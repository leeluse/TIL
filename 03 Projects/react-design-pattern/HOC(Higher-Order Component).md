---
aliases:
  - design-pattern
tags:
  - design-pattern
---
HOC는 고차 컴포넌트를 의미하는데, Javascript의 고차 함수(Higher-Order Function)이랑 비슷한 개념이다
컴포넌트 로직을 재사용하기 위한 React의 고급 기술로, 특정 패턴이다
컴포넌트를 받아서, 기능이 추가된 새로운 컴포넌트를 반환하는 함수이다

### 코드 예시
---
```tsx
const EnhancedComponent = withSomething(Component);
```

예를 들어 권한 체크를 여러 페이지에서 계속 해야 한다고 할 경우

```tsx
function AdminPage() {
	const role = useRole();
	
	if (role !== "admin") {
		return <>권한이 없음</>
	}
	return <>관리자 페이지</>
}
```

위와 같은 코드가 페이지마다 반복되는 것이 번거로울 경우 `HOC`로 뺄 수 있다

```tsx
function withAdmin(Component) {
	return function AdminComponent(props) {
		const role = useRole();
		
		if(role !== "admin") {
			return <>권한이 없음</>
		}
	}
	return <Component {...props} />;
}
```

함수 컴포넌트에 컴포넌트를 전달 받아서, 컴포넌트를 반환해 줄 수 있다
반환하는 컴포넌트 내부에서 권한 체크를 진행한다


```tsx
function AdminPage() {
	return <div>관리자 페이지</div>; 
} export default withAdmin(AdminPage);
```


### 연결
---
- [[구현 상세 추상화하기]]