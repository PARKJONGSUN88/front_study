## react Route

#### route

리액트의 기본 모드는 cra에서는 기본적으로 페이지를 이동하는 routing을 위한 로직이 없다.

그래서 추가적으로  [react-router](https://reacttraining.com/react-router/web/guides/quick-start) 를 설치하여 페이지 이동을 하였다.

!! 이런것만 봐도 리액트가 자유도가 높다는 말을 알 수 있다. 기본 route를 위한 것도 추가로 골라서 설치한다니.



```jsx
//Route.js 파일을 만들었다. index.js외 Route를 관리하는 js이 되는 것이다.

import React, { Component } from "react";
import { BrowserRouter as Router, Route, Switch } from "react-router-dom";
import Main from "./pages/Main/MainPageApp";
import Login from "./pages/Login/LoginPageApp";
import Signup from "./pages/Signup/SignupPageApp";


class Routes extends Component {
  constructor() {
    super();
  }    
  
  render() {
    return(
      <Router>
        <Switch>
          <Route exact path="/main" component={Main} />
          <Route exact path="/" component={Login} />
          <Route exact path="/login" component={Login} />          
          <Route exact path="/signup" component={Signup} />
        </Switch>
      </Router>
    )
  }
}

export default Routes;
```



```jsx
//Route.js 

import React from 'react';
import ReactDOM from 'react-dom';
import "./styles/common.scss";
import "./styles/reset.scss";
// import MainPageApp from './pages/Main/MainPageApp';
// import LoginPageApp from './pages/Login/LoginPageApp';
// import LoginPageApp from './pages/Signup/SignupPageApp';
import Routes from "./Routes";

// ReactDOM.render(<MainPageApp />, document.getElementById('root'));
// ReactDOM.render(<LoginPageApp />, document.getElementById('root'));
// ReactDOM.render(<SignupPageApp />, document.getElementById('root'));
ReactDOM.render(<Routes />, document.getElementById('root'));
```



Route.js 파일 추가 후 index.js는 변경되었다. 

이제 직접적으로 페이지들을 관리하는게 아니라 Route.js를 통해 선택된 페이지를 받겠다는 것이다.



```jsx
//Login.js

import React, { Component } from "react";
import { withRouter } from 'react-router-dom';
import "./LoginContentsBoxFirst.scss";

class LoginContentsBoxFirst extends Component {
    
  // 로고 누를시 goToDirect()함수실행으로 "/"로 이동 함수 //
  goToDirect() {
    this.props.history.push('/');
  }
    
    render() {
    return(
        //goToDirect()를 사용한 부분 
          )
  }
}

export default withRouter(LoginContentsBoxFirst);    
```





#### route로 이동하는 두가지 방법.

**Link 컴포넌트를 사용하는 방법**

Routes에서 설정한 path로 이동하도록 구현하려면 `Link` 컴포넌트를 사용합니다.

```jsx
import React from 'react';
import { Link } from 'react-router-dom';

class Login extends React.Component {
  render() {
    return (
      <div>
        <Link to="/signup">회원가입</Link>
      </div>
    )
  }
}

export default Login;
```

그런데 react-router-dom에서 제공하는 Link 컴포넌트는 dom에서 `` 로 변환되므로, 혹시 a태그를 사용하고 싶지 않다면 Link를 사용하지 않으셔도 됩니다. (예를 들어 이미 다른 태그로 버튼 컴포넌트를 만들어 놓았을 경우..)



**withRouter HOC로 구현하는 방법**

Link를 사용하지 않고, 요소에 onClick 이벤트를 달아서 이동하고 싶은 곳으로 넘기는 방법도 있습니다. 아래 goToSignup 라는 event handler에서 구현한 것처럼 this.props의 history에 접근해서 이동할 수 있습니다.

받은 history의 push 메서드에 이동할 path를 인자로 넘겨주면, 해당 라우트로 이동할 수 있습니다.

```jsx
import React from 'react';
import { withRouter } from 'react-router-dom';

class Login extends React.Component {

  goToSignup() {
    this.props.history.push('/signup');
  }

  render() {
    return (
      <div>
        <div
          class="btn signup-btn"
          onClick={this.goToSignup.bind(this)}
        >
          회원가입
        </div>
      </div>
    )
  }
}

export default withRouter(Login);
```

이 컴포넌트에서 props에 route 정보(history)를 받으려면 export하는 class에 `withRouter`로 감싸주어야 합니다. 이렇게 withRouter같이 해당 컴포넌트를 감싸주는 것을 [higher-order component(이하 HOC)](https://reactjs.org/docs/higher-order-components.html) 라고 합니다.

HOC는 react 고급 기능입니다. 기능이라기보다는 컴포넌트의 공통부분을 구현하는 패턴이라고 생각하시면 됩니다. 간단히 설명하면 HOC는 함수입니다. 그런데 컴포넌트를 인자로 받고, 컴포넌트를 return하는 함수입니다.
