## styled-component에서의 코드 품질 향상을 위한 고민

나는 요즘 개인프로젝트로 React UI 컴포넌트 프로젝트를 하고 있다. 프로젝트라기보다는 개인적으로 좋아하는 UI부분이기에 취미?로 하고 있다. React, TypeScript, Styled-Component를 활용한다. 

github: https://github.com/PARKJONGSUN88/React-ui-js

<br>

그런데 개발을 하던 중 코드 리펙토링 중 리뷰를 해보고자 하는 부분이 생겨서 이렇게 글을 남긴다.

styled-component는 컴포넌트답게 

 - props를 받아 사용할 수 있으며 
 - 리터럴 문법을 활용해 JS문법을 사용가능하기에 함수를 사용할 수 있게 된다. 

<br>

**너무 매력적인 부분이다.** 스타일도 ~~스타일리쉬하게~~.. 보다 프로그래밍 언어답게 작성한다. 

css는 ~~노가다~~.. 단순 반복 작업이라 생각하던 이들에게 꼭 사용해보라고 말하고 싶다.

<br>

styled-components라이브러리를 활용하는 가장 기본은 `styled` 요소이다. 

이 부분은 많은 글들이 있으므로 나는 `keyframes`, `css`에 대하여 말하여 보자 한다.

```tsx
import styled, { keyframes, css } from 'styled-components';
```

<br>

<br>

<br>

이번에 프로젝트를 진행하다가 일부를 가져왔다. 

###  최초 코드

```tsx
const Items = styled.div<ItemsType>`
  flex-direction: ${(props) => props.direction};
  width: ${(props) => props.direction === 'column' ? props.width : props.width * props.count}px;
  height: ${(props) => props.direction === 'column' ? props.height * props.count : props.height}px;  
  animation: ${(props) => props.direction === 'column'
        ? onMove(
            (props.height * props.count) - (props.height * 0.25),
            (-1 * props.ViewHeight) + (props.height * 0.25)
          )
        : onMove(
            (props.width * props.count) - (props.width * 0.25),
            (-1 * props.ViewWidht) + (props.width * 0.25)
          )
	  }
    ${(props) => (props.toggle ? 'running' : 'paused')}
    ${(props) => props.speed}s;
`;
```

<br>

### 리펙토링

```tsx
const Items = styled.div<ItemsType>`
  ${({direction, width, height, count, ViewWidht, ViewHeight, speed, toggle}) => {
    if (direction === 'column')
      return css`
        width: ${width}px;
        height: ${height * count}px;
        flex-direction: ${direction};
        animation: ${onMove(
            (height * count) - (height * 0.25),
            (-1 * ViewHeight) + (height * 0.25)
          )}
          ${speed}s 
		  ${toggle ? 'running' : 'paused'};
      `;
    else
      return css`
        width: ${width * count}px;
        height: ${height}px;
        flex-direction: ${direction};
        animation: ${onMove(
            (width * count) - (width * 0.25),
            (-1 * ViewWidht + width * 0.25)
          )}    
		${toggle ? 'running' : 'paused'}
  		${speed}s;
      `;
  }};
`;
```

<br>

<br>



### 1. 첫번째 - 비구조화할당
props를 받아오는 부분에 대한 변화. 

마치 본 component에서 비구조화할당을 한 것과 같이 styled-component에서도 props의 요소들은 비구조화할당 하여 사용하였다. 

```tsx
${(props) => {props.name}}
```

처음에는 함수를 선언하는 부분의 파라미터로 하여 그 파라미터의 객체로써 props를 받아서 사용하였었다. 그리고 그 props의 key값들을 일일이 지정하 필요한 곳에 작성하였다.

```tsx
${({name}) => {name}}
```

비구조화할당을 하여 파라미터의 값들을 일일어 지정해놓고 바로 사용한다.

<br>

**결론**

처음 함수를 정의할 때는 당연히 일일이 그 요소들을 꺼내?서 쓰는 것보다는 하나의 파라미터이름으로 선언해서 사용하는 것이 깔끔하다고 생각하였다. 그러나 그 객체 안에 요소들이 많을 경우 그것을 사용하기 위해 일일이 객체명.key값으로 하는 것보다 깔끔할 수 있다고 생각하였다.

<br>

<br>

### 2. 두번째 - 비교문 줄이기, 그리고 css의 사용

반복되고 중첩되는 비교문의 사용량을 줄일 수 있는 방법을 생각하였다.

품질 향상을 위한 많은 방법 중 시간복잡도에 것을 들어본 적이 있다. 

<br>

**시간의 복잡도란?**

**알고리즘을 구성하는 명령어들이 몇번이나 실행됬는지 센 결과(frequency count)**

**각 명령어의 실행시간(execution time)** 을 곱한 합계를 의미함!!!

<br>

사실 나는 아직 정확하게 이 것까지 고민하며 개발을 할 수 있는 단계가 아니다.

그러나 나는 리펙토링을 시작하게 된 이유가 바로 이것이었다.

<br>

**최초코드에서는** 

```tsx
${(props) => props.direction === 'column' ? 1번 : 2번}
```

이 비교문. 

그러니까 "direction" props가 무엇이냐에 따라 어떤 것들을 실행할지를 작성했는데 이 비교문에 의한 실행할 것들이 각각 흩어져 있다. 스타일을 위한 스타일 프로퍼티마다 작성되어 있다. 

**그만큼 각각 실행이 된다는 것이다**.

```tsx
flex-direction: ${(props) => props.direction}; // 1번
width: ${(props) => props.direction === 'column' ? props.width : props.width * props.count}px; // 2번
height: ${(props) => props.direction === 'column' ? props.height * props.count : props.height}px; // 3번
animation: ${(props) => props.direction === 'column' ? ...  // 4번
```

<br>

**리펙토링 후에는**

```tsx
${({direction, width, height, count, ViewWidht, ViewHeight, speed, toggle}) => {
    if (direction === 'column')
      return css`
        //실행내용
      `;
    else
      return css`
     	//실행내용
      `;
```

한번의 비교문으로 여러 스타일 프로퍼티를 실행하도록 하였다. 함수 선언부의 프로퍼티의 객체 key값을 비구조화할당을 하여 사용한 부분도 보인다. 선언부에서는 오히려 이 부분이 지저분해 보일 수도 있으나 실행내용 쪽을 보면 더욱 깔끔하다.

<br>

그리고 여기서 또 하나의 내용은 `css`의 사용이다.  이 것을 왜 썻을까? 나는 그 장점을 "값 유추를 바로 하게 해준다."라고 말하겠다.

<br>

**`css` 없이 일반적으로 작성할 경우**

```tsx
return 'width: 100px; height:50px; flex-direction:row';
```

return 후 그 값들을 모두 string으로 하여 styled-component의 값으로 주는 것인데 여러 요소들을 한번에 작성하다보면 마치 inline스타일링을 하는 것처럼 그 값들을 모두 string으로 작성하여야 한다.

```tsx
return `width: ${width}px; height:${height}px; flex-direction:row`;
```

물론 리터럴문법으로 중간에 함수를 사용하는 것은 가능하다.

<br>

**`css` 사용하여 작성**

```tsx
return css`
        width: 100px;
        height: 50px;
        flex-direction:row;        
      `;
```

return 후 그 값들을 다시한번 css의 프로퍼티로써 받고 그 뒤의 값들을 받는다. inline처럼 string으로 주는 것이 아닌 css를 작성할 때 프로퍼티로 작성하다보니 그 이점은 값 유추(~~자동완성 굿~~)를 사용 할 수 있다. 또한 모든 값을 string으로 다 작성하면서 개발하는 것보다는 편했다. 나는.

```tsx
return css`
        width: ${width}px;
        height: ${height}px;
        flex-direction:row;        
      `;
```

물론 기본이 리터널문법이므로 안에 함수를 사용할 수 있다.

<br>

**결론**

처음에는 각각의 스타일컴포넌트 프로퍼티들 마다 함수를 사용하여 그 값을 작성하였다. 그러나 만약 어떤 한 값에 의한 의존되는 값들이 많을 경우 이처럼 하나의 비교문에 의한 결과를 내는 것도 좋은 방법이 된다고 생각한다.

<br>

<br>

### 3. 세번째 - keyframes의 사용법에 관하여

```tsx
animation: ${(props) => (props.isToggle ? 'onScale' : 'offScale')};
@keyframes onScale {
    0% {
      transform: scale(0);
    }
    100% {
      transform: scale(1);
    }
}
@keyframes offScale {
    0% {
      transform: scale(1);
    }
    100% {
      transform: scale(0);
    }
}
```

내가 예전 프로젝트를 할 때 styeld-component에서 애니메이션을 위해 keyframes을 사용한 코드이다.

그런데 사실 onScale과 offScale은 그 로직이 큰 차이가 아니다. 

단순 작동을 on하거나 off시키는 것인데 그를 위해 2개의 `@keyframes`이름이 사용되었다.

<br>

저 당시 뭔가 비슷한 함수 2개를 사용하는 것과 같아 좀 의심쩍은 부분이었기에 이번 프로젝트에서는 다른 방법을 고민하였고 그뒤에 새로운 방법으로 작성해보았다.

```tsx
// 함수표현식으로 표현한 부분
const onMove = (e: number, i: number, y: number, z: number) => keyframes` 
  0% {
    transform: translate(${y}px, ${e}px);
  }
  100% {
    transform: translate(${z}px, ${i}px);
  }
`;

// 사용한 부분
return css` 
	animation: ${onMove(
    	(height * count)- (height * 0.25),
    	(-1 * ViewHeight) + (height * 0.25),
    	0,
    	0,
	)};       
`;
else return css`
	animation: ${onMove(
    	0,
    	0,
    	(width * count) - (width * 0.25),
    	(-1 * ViewWidht) + (width * 0.25),
	)}
`;
```

하나의 keyframes함수를 사용하여 지정된 프로퍼티 위치에 그때마다 다른 값을 넣어주도록 하였다. 

그때마다 프로퍼티의 값들을 props로 받아와 변하게 하는 점도 중요하지만 

여기서는 **프로퍼티의 위치**에 따라 **하나의 함수로 on, off 하는 로직**을 만들었다는 것에 의미를 두고자 한다.

<br>

별 것이 아닌 것처럼 보일 수 있지만 이는 하나의 keyframes변수를 덜 작성한 것하였고

만약 아래도 함수형이 아니었다면 4개의 keyframes변수가 필요했을지도 모른다.

이는 성능적으로도 차이가 날 수 있다는 것이다.

 

