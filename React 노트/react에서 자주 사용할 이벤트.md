## react에서 자주 사용할 이벤트



#### map, 반복되는 값들을 뿌려줄 때 사용하는 array의 메소드

리스트페이지가 있다고 할때 리스트의 하나를 그려주는 자식요소 component

그리고 그 자식요소를 반복적으로 뿌려줄 list component로 구성했다.

```jsx
// comment.js
import React, { Component } from "react";
import "./Comment.scss";

class Comment extends Component {
  constructor() {
    super();
  }

  render() {
    return(
      <p className="commentText">
        <b>{this.props.name}</b>
        <span>{this.props.text}</span>
      </p>
    )    
  }
}

export default Comment;


// commentList.js
import React, { Component } from "react";
import "./CommentList.scss";
import Comment from "../Comment/Comment";

class CommentList extends Component {
  constructor() {
    super();

  }

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
}

export default CommentList;
```

comment.js에서는 **가장 기본단위로** 한개의 댓글을 그려준다.

comementList.js에서는 댓글 data(json)을 가져와 comment.js형식으로 반복적으로 그려준다.



그 그려주는 것이 바로 map. array의 내장메서드를 이용하는 것이다.

왜 map을 사용해야되는지는

 [https://velog.io/@jongsunpark88/state-%EB%8D%B0%EC%9D%B4%ED%84%B0%EC%9D%98-%EC%83%81%ED%83%9C.-%EB%8D%B0%EC%9D%B4%ED%84%B0%EC%9D%98-%EA%B0%92%EC%9D%B4-%EB%B3%80%ED%95%98%EB%8A%94-%EC%A0%80%EC%9E%A5%EC%86%8C](https://velog.io/@jongsunpark88/state-데이터의-상태.-데이터의-값이-변하는-저장소) 

map에 관한 자세한 사용법은 공식문서로..





#### 삼항연산자를 이용하여 switch식 스타일 이벤트 사용하기

```jsx
// .js
this.state = {
      memCheck: true
}

	  render() {
    return (
      <div className="LoginPage">
        <div className="LoginPage-wrap">
          <div className="loginLogo">
            <h2>Log In</h2>
          </div>
          <ul>
            <li
              onClick={this.liFunc.bind(this)}
              className={this.state.memCheck ? "trueli" : "falseli"}
            >
              <span>회원로그인</span>
            </li>
              
              
// .scss
              .trueli {
                  border: 1px solid #999;
                  border-bottom-color: #fff;
                  background-color: #fff;
                  transition: ease-in-out 0.3s;
                  pointer-events: none;
              }
              .falseli {
                  border: 1px solid #e5e5e5;
                  border-bottom: 1px solid #e5e5e5;
                  border-bottom-color: #999;
                  background-color: #f6f6f6;
                  color: #727272;
                  transition: ease-in-out 0.3s;
              }
```

state의 값을 boolean으로 하여 스위치처럼 사용할 수 있다.

그러면 그 것을 활용하여 **className의 삼항연산자**를 적용하여 간단하게 스타일을 변경할 수 있다.

필요한 경우 하나의 state값을 활용하여 여러개의 스위치를 껏다 킬수도 있다.

- 버튼의 색이 변한다거나, div가 사라졋다 나타난다든가 여러가지로 활용 가능




