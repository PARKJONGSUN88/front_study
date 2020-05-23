## state

#### state 데이터의 상태. 데이터의 값이 변하는 저장소.

```jsx
this.state = {
      name:"접속자 이름",
      comment:[
        {commentWriter:"친구1", commentText:"친구의 첫번째 댓글"},
        {commentWriter:"친구2", commentText:"친구의 두번째 댓글"}     
      ],
      text:"", // 댓글창에 text onChange용 state //
      TextValidateCheck:false // 댓글 input값 없는 것 유효성검사용 state //       
}
```

리액트는 state의 변화가 일어날때 render가 일어난다. 
**render가 일어난다는것?** 화면의 보이는 것이 변한다는 것이다. 그리고 그건 웹브라우저가 일을 한다는 것이다.



요즘 웹페이지에서는 한부분이 변한다고 해서 모든 페이지가 리로딩되거나 리다이렉트 되지 않는다.

state는 render를 반영시키는 요소이지만 유저에게 직접적으로 보이는 요소는 아니다.  

하지만 유저의 input이나 유저에게 output후 state 상태값은 변할 수 있다.

(아니 계속 변할 것이다. 정적페이지가 아닌 이상 최초 state에서 변하지 않으면 state를 사용할 이유가 없다. 

고정변수, 상수값으로 컴포넌트에 넣은게 아닌 이상 말이다.) 



우선 state는 마치 객체와 같이 생겼다. state안에는 원하는 키값을 지어주고 그 안에는 원하는 밸류값처럼 지정을 해줄 수 있다. 그리고 또한 그 밸류값은 객체처럼 string, array, boolean, number까지 다 가능하다.

```jsx
name:"접속자 이름" // string으로 해서 값을 저장 및 사용할 예정이다.
```



```jsx
 constructor() {
    super();
    
    this.state = {    
      text:"", // 댓글창에 text onChange용 state //
      TextValidateCheck:false // 댓글 input값 없는 것 유효성검사용 state //
    }    
  }
```

state는 생성자(constructor)에 위치한다. 직접적으로 class안 함수나 render메서드 안이 아니다.

state는 불변성을 유지한다. !! 이유는 리액트의 성능향상과 관련되있다. 리액트의 규칙이다. 

그런데 그냥 규칙이라고 넘어가면 안되고 이해를 해보면



참고: [https://medium.com/@ljs0705/react-state%EA%B0%80-%EB%B6%88%EB%B3%80%EC%9D%B4%EC%96%B4%EC%95%BC-%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0-ec2bf09c1021](https://medium.com/@ljs0705/react-state가-불변이어야-하는-이유-ec2bf09c1021) 



리액트는 render를 통해 그림을 다시 그린다. 그런데 그걸 반영해야 되는 것이 state의 값들이다. 

state의 값을 바꾸면 그 변화를 리액트가 감지하는게 성능과 연결되있다는 뜻임.



그래서 state를 직접적으로 값을 수정하길 권하지 않는다.



#### setState

그러면 state는 활용하라고 있는것인데 뭘로 사용하느냐?

react에서 제공하는 state값을 변화시키는 메서드인 setState이다.

```jsx
textValidateFunc() {
    if(this.state.text.length !== 0) {
      this.setState({TextValidateCheck:true}, () => console.log("유효성:", this.state.TextValidateCheck))
    } else {
      this.setState({TextValidateCheck:false}, () => console.log("유효성:", this.state.TextValidateCheck)) 
    }
  }
```

setState로 boolean의 값을 변경해주었다.그외 string이나 다른 형태도 마찬가지다.

그런데 array는 알아야 될것이 있다.

만약 array를 썻다는건 그 안의 값들이 여러개가 있을 것이라는 것이다. 그런데 setState로 array를 변화시킬수 있을까? array의 요소를 더하거나 빼거나가 될것인가?



**안된다**...

배열같은 경우는 그 배열에 직접적으로 값을 추가하는 push, pop등 다 불가능하다. 불변성유지때문이라고.

그러면 활용을 어떻게 해야되는지?





#### array.map, concat, filter

그것은 array의 메서드 중 기존 원 배열은 건들이지않고 원 배열에 새로운 값을 추가햐 새값을 내놓는 map메서드가 있다. map메서드를 활용해야 한다.

map, filter, concat등 직접적으로 원 배열값을 건드는 것이 아닌 새값을 내놓는 메서드를 말이다



```jsx
render() {
    return(
      <div className="comment-view-div">
        {
          this.props.comment.map((item, inx) => {
            return (
              <Comment key={inx} name={item.user_id} text={item.user_comment} />
            )
          })
        }
      </div>     
    )
  }
```



