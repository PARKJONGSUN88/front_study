## fetch. 서버와의 데이터를 통신하기 위한 함수 + HTTP

### HTTP 통신에 대해

#### HyperText Transfer Protocol
하이퍼텍스트(HTML) 문서를 교환하기 위해 만들어진 protocol(통신 규약).
즉 웹상에서 네트워크로 서버끼리 통신을 할때 어떠한 형식으로 서로 통신 규약
프론트앤드와 백엔드간에의 통신에서도 사용된다.

#### HTTP는 Stateless 이다.
Stateless 란 말그대로 state(상태)를 저장하지 않는 다는 뜻.
즉, 요청이 오면 그에 응답을 할뿐, 여러 요청/응답 끼리 연결되어 있지 않다는 뜻이다. 즉 각각의 요청/응답은 독립적인 요청/응답 이다.
예를 들어, 클라이언트가 요청을 보내고 응답을 받은후, 조금 있다 다시 요청을 보낼때, 전에 보낸 요청/응답에 대해 알지 못한다는 뜻이다.
그래서 만일 여러 요청과응답 의 진행과정이나 데이터가 필요할때는 쿠키나 세션 등등을 사용하게 된다.



### fetch

웹브라우저(프론트엔드)에서 정보를 입력받았다.
그러면 그 정보를 서버로 보내줘야 한다.

#### 요청(request), 응답(response)

기본적으로 http는 요청(request), 응답(response)가 한 세트다.
그러면 그것을 어떻게 해야되느냐. 그 중 한 방법이 fetch함수(javascript내장함수이다)를 이용할 것이다.

```jsx
/// post용 ///

// fetch 후 alert 메세지용 //
  welcomeAlert() {alert("westagram 회원이 되신 것을 축하드립니다!")}
  alreadyUserAlert() {alert("이미 존재하는 회원입니다.ㅠㅠ")}
  serverErrorAlert() {alert("알 수 없는 오류가 발생했습니다.")}
  
  // signup에서 login으로 이동시킬 fetch 함수 //
  goToLogin() {
    fetch('http://10.58.4.56:8000/account/signup', {
      method: "POST",
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        "email": this.state.email,
        "username": this.state.name,
        "password": this.state.password               
      })
    })    
    .then(res => {
      if (res.status === 200) {
        this.welcomeAlert();
        this.props.history.push('/'); 
      }
      if (res.status === 401) {
        this.alreadyUserAlert();
      }
      if (res.status === 400) {
        this.serverErrorAlert()
      }     
    })    
  }

/// get용 ///
 fetFunc() {
    const token = localStorage.getItem('token');
    fetch("http://10.58.1.192:8000/comment", {
      headers: {
        "Authorization":token,
      }
    })
    // .then((res) => console.log(res))
    .then((response) => response.json())
    .then((res) => this.setState({comment:res.data}, () => console.log(this.state)))
  }


```

회원가입을 위한 js파일인데 이렇게 구성하였다.  

fetch함수는 우선 프론트엔드에서 서버로 보내는 함수다.

서버와 서버가 데이터를 주고받는것은 여러포맷의 문서가 있지만 현재는 json만을 생각한다. 



fetch()안에 보낼 것들을 넣어 보낸다.  기본적으로 get,post. 어떤 method방식으로 보내더라더 필수로 필요한 것은 받을 주소(url)이다. 



받을 주소는 url =

http프로토콜+도메인주소(또는 ip주소)+포트(도메인의경우 기본설정되면 생략될 수도)+엔드포인트이다.



그리고 HTML과 비슷하게 header, body로 나누어져 있고, 또한 비슷하게 header는 메타 데이터, body는 전달할 데이터 라고 보면 된다.



우선 요청을 하면 다시 응답을 받는다. 그 응답을 받는 방법이 .then() 메서드이다. 

.then() 

then도 함수임. promise 함수이다. 그리고 함수니까 인자가 들어갈 수 있다.

그러니까 then(인자값 => 인자를 돌려라)가 된다.  그리고 .json()도 비동기함수다.

then() 메서드는 promise를 리턴하는것인데. 즉 fetch로서 요청을 하고 **응답이 왔을 때**라는 약속을 하는 것임.

```jsx
fetch("http://10.58.1.192:8000/comment")
    .then((response) => response.json()) //여기서 then은 fetch에 대한 then임
    .then((res) => this.setState({data:res}, () => console.log(this.state)))
// 여기서 .then((res) => )에서의 (res)는 화살표함수의 앞 ()임

// 여기서 then은 json()에 대한 then임

// 하지만 로그인 할때는 token
.then((res) => localStorage.setItem("token", res.token))

```



### promise

promise에 대해서는

참고: https://joshua1988.github.io/web-development/javascript/promise-for-beginners/ 



### get과 post의 차이

get과 post의 차이에 대해서는

참고: https://hongsii.github.io/2017/08/02/what-is-the-difference-get-and-post/ 



**그리고 중요한점.** 서버와의 응답시 만약 나는 json형태로만 주고받고자 하는데 서버는 http형식만을 추구한다면 서로 데이터 전달이 안될 수 있다. 

```jsx
 body: JSON.stringify({
        "email": this.state.email,
        "username": this.state.name,
        "password": this.state.password               
      })
```



### JSON.stringify

JSON.stringify는 자바스크립트의 값을 JSON 문자열로 변환하는 메소드다.

header부분은 json화 하지 않아도 서버에서 해석을 할수가 있기에 JSON.stringify를 안해도 되지만 바디의 보낼 데이터부분은 JSON.stringify를 하여 서버로 전송해야 서버에서 전달받을 수 있다.



그리고

```jsx
  headers: {
        "Authorization":token,
      }
    })
    // .then((res) => console.log(res))
    .then((response) => response.json())
```

get요청에서 json()를 살펴봐야한다.

이것은 응답이 왔을 때 그 응답을 json에서 자바스크립트화 하겠다고 할 수 있다.

만약 http status code만이 필요하면 http응답을 바로 읽으면 되지만. 만약 status코드가 아니라 바디에있는  내용이 필요한것이라면 json()메서드로 응답온것을 javascript화 한다.

**!!!!사실 정확히 말하면 json()메서도는 javascript화라기 보다는 스크림을 기다렸다가 다 끝나면 json으로 만들어서 읽게 해준다는 것**



### json()에 대해서

참고:  https://wooooooak.github.io/javascript/2018/11/25/fetch&json()/ 

한마디로 아직 바디안에 있는 내용이 다 로딩이 안되서 사용할 수 있는 상태가 아니라는 것.



**! 만약 응답을 json()해놓고 status를 확인하고자 하면 안나올수 있다. 왜냐하면 이미 자바스크립트화되어 status 코드를 볼수가 없기 떄문이다.**



그리고 이 json() 메소드 또한 promise형태이다.

그래서 

```.then((response) => response.json())```으로 데이터 읽을 수 있게 되면 읽고

```.then((res) => setState())``` 여기서 res는 json()에 대한 promise다.



#### 토큰

```jsx
goToMain() {    
    const token = localStorage.getItem('token');  
    //토큰으로 받아온 값은 로컬스토리지에 저장되있으며 변수로 지정하였다.
    fetch("http://10.58.1.192:8000/account/signin", {
      method:"POST",
      headers: {
        "Authorization":token,
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        "email": this.state.email,
        "password": this.state.password      
      }),
    })   
    .then(res => {
      if (res.token) { //여기서 res는 내가 지정한 응답의 이름이고, 그 안의 객체로 또 정보가 있음
          //"token"이라고 서버에서 지정한 키 이름인 것임.
        localStorage.setItem(token, res.token); //토큰을 받으면 로컬스토리지에 셋(넣어라.)
      }
      if (res.status === 200) {
        alert(`${this.state.email}님 환영합니다.`)
        this.props.history.push('/main'); 
      }
      if (res.status === 401) {
        alert("회원 정보를 다시 확인해주세요ㅠㅠ")
      }
      if (res.status === 400) {
        alert("먼저 회원가입을 해주세요")
      }     
    })   
  }
```

로그인에서는 post방식을 보낸 후에 응답에 바디가 있다. 보통은 post 방식은 응답에 바디가 없지만  login은 token을 받아오고 그 token을 이용하여 로그인 된 유저가 그 유저라는 인증이 된 상태로 페이지 이동이나 서비스를 이어간다.

  ```"Authorization":token,```로 서버에 인증값은 토큰(내가지정한 변수명)을 같이 보내는 것이다.

 그러면 서버에서는 데코레이터(decorator)를 통하여 해당 유저가 이미 로그인(인증)된 유저임을 알고 그에 맞는 응답을 주는 것이다.



