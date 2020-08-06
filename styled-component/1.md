## styled-component에 대하여

스타일을 컴포넌트화한다.

예전처럼 html, js, css를 따로 작성하고 관리하는 것이 아닌 

컴포넌트 단위로 관리하기 위해 스타일 또한 한 컴포넌트에 함께 작성한다.

 

```jsx
import styled from "styled-components";

//React 컴포넌트
const Component = () => {
    return (
    	<>
        	<Styled />
        </>
    )
}

export default Component;

//스타일 컴포넌트
const Styled = styled.div``;
```

jsx 문법을 사용한 컴포넌트 내용에서 마치 또하나의 컴포넌트처럼 선언하고 그 내용을 ``styled.tag``로 하여 원하는 html 태그를 사용한다.



태그 선언 뒤 백틱을 이용하여 태그에 적용할 스타일을 적용할 수 있다.
```jsx
const Styled = styled.div`
	width:100px;
`;
```



스타일 **컴포넌트** 답게 props를 이용하여 재사용을 할 수가 있다.

이때 리터럴문법을 이용하여 백틱사이에 자바스크립트 문법을 쓸수 있는것을 사용하는 것이다.

```jsx
return (
    	<>
    		//컴포넌트를 정의하는 것이다. 그리고 컴포넌트기에 props를 전해줄 수 있다.
        	<Styled color={"빨강"} />        
        </>
    )

//스타일 컴포넌트 정의
const Styled = styled.div`
	${자바스크립트문법}
`;
```

```jsx
// 백틱 안에서 함수를 사용한다
const Styled = styled.div`
	${() => {}}
`;
```

```jsx
// 화살표함수를 사용해서 간결히 했으며 위 컴포넌트에서 전달해준 props를 받는다.
const Styled = styled.div`
	${(props) => props.color}
`;
```

```jsx
// props내용을 함수에서 받았다. 함수의 return값기 때문에 결과로 생각하면 "빨강" 이다.
// css파일에서 string "빨강"만 있으면 아무것도 아닐 것이다.
// 그러나 프로퍼티의 값으로써 적절한 위치만 있으면 그 것이 value로써 적용된다.
const Styled = styled.div`
	"빨강"
`;
```

```jsx
// background-color의 프로퍼티의 value로써 함수를 호출한 return값을 받는다.
const Styled = styled.div`
	background-color:${(props) => props.color};
`;
```
```jsx
// 실제로 모든 과정이 끝나면 일어날 결과
const Styled = styled.div`
	background-color:"빨강";
`;
```



응용

```jsx
// 삼항연산자를 이용한 동적 사용이 가능하다.
// props.color에 값이 있으면 그것을 대입하고 아니면 "파랑"을 대입한다.
const Styled = styled.div`
	background-color:${props => props.color ? props.color : "파랑"};
`;
```



## 타입스크립트 스타일컴포넌트

```tsx
interface ComponentType {
  bWidth?: number;
  bHeight?: number;
}

interface ButtonType {
  bWidth: number;
  bHeight: number;
}

const Component:React.FC<ComponentType> = ({
  bWidth = 100,
  bHeight = 100,
}) => {
    return (
 		<Button bWidth={bWidth} bHeight={bHeight} />
	)
}

export default Component;

const Button = styled.div<ButtonType>`
  width: ${(props) => props.bWidth}px;
  height: ${(props) => props.bHeight}px;
  transform: translateX(${(props) => props.bWidth / 2}px);
`;
```

스타일 컴포넌트도 **컴포넌트**기에 타입을 선언해줘야 한다.

코드를 보면 React 컴포넌트를 정의 후 return에서 ``Button``이라는 스타일 컴포넌트를 선언하고 props를 내려주고 있으며 

다시 스타일 컴포넌트를 정의하고 정의시에 타입을 선언해주고 사용하고 있다.



스타일 컴포넌트를 활용하면 동적으로 변하는 스타일을 적용하기 좋고 컴포넌트로 단위로 스타일과 스크립트, html을 작성하기에 

컴포넌트적으로 사용하기에 좋다.

