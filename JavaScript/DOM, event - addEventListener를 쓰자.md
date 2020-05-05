## DOM, event - addEventListener를 쓰자



#### 1. javascript에서 이벤트를 처리하는 방법에는 3가지가 있다.

##### 1. HTML 요소에 직접 이벤트 초리기 속성을 설정.
```html
<inout type="button" onclick="buttonClick()">
```
이 경우 직접적으로 HTML상에 함수를 실행하라고 명시하는것인데
**가독성이 떨어지고 이벤트를 단 하나밖에 지정할 수 없다는 단점이 있음.**
<br>


##### 2. DOM 요소 객체의 이벤트 처리기 프로퍼티에 설정.
```javascript
var btn = document.getElementById("button");
btn.onclick = buttonClick();
```
우선 DOM을 이용해 요소를 get한다. 그리고 그 변수를 이벤트 처리기의 프로퍼티로 사용했다.
위에서 "btm." 뒤의 "onclick"이 프로퍼티임. 프로퍼티에서는 addEventListener처럼 "click"아 이닌 "on"을 붙인 "onclick"이다.

**위의 방법보다는 script와 html이 분리된 코드. 그러나**
**특정 요소의 특정 이벤트에 대해서 이벤트 처리기를 단 하나만 등록할 수 있는 단점이 있다.**
<br>


##### 3. addEventListener 메서드를 사용.

addEventListener는 메서드임.. 원하는 요소에 메서드로 함수에 등록하는 것.

**같은 요소에 같은 이벤트를 여러 개 등록할 수 있다는 것!**

**즉, 위의 두 방법보다는 이 방법이 가장 좋다고 할 수 있음.**

<br>




#### 2. 직접 만든 westagram에 addEventListener 적용

##### 1. 코드 정리 전

```javascript
addEventListener('keyup', function() {
    let comment = document.getElementsByClassName("comment-write")[0].value;
    if (comment.length !== 0) {
        document.getElementsByClassName("submitButton")[0].classList.add("clickbutton");
    }
});
// 처음에는 addEventListner를 사용하였지만 따로 어떤 함수에 지정하지 않고 
// addEventListner안에 변수부터 DOM요소까지 모두 작성하였었음.

let superUser = "js_Park"
function commentWrite() {
    let result = document.getElementsByClassName("comment-view-div")[0];
    let btag = document.createElement("b");
    btag.innerHTML = superUser;
    let commentText = document.getElementsByClassName("comment-write")[0].value;
    let commentViewSpan = document.createElement('span');    
    commentViewSpan.innerHTML = commentText;
    let brtag = document.createElement("br");
    result.appendChild(btag);
    result.appendChild(commentViewSpan);
    result.appendChild(brtag);  
}
// 기능 구현에 있어서도 다른 기능과의 중복되는 코드(같은 DOM요소 등)가 있었음.
// 그리고 함수를 html상 태그에 직접적으로 이벤트 처리기를 설정했었음. 

let enterPass = document.getElementsByClassName("comment-write")[0];
enterPass.addEventListener('keydown', function(e) {
    if (e.keyCode === 13 ) {
        commentWrite();
    }
})
```



##### 2. 코드  정리 후

```javascript
/* 댓글 게시 버튼 요소겟 */
const submitButtonClick = document.getElementsByClassName("submitButton")[0];
const commentDone = document.getElementsByClassName("comment-write")[0];
// 여러 기능들에서 쓰일 변수들은 전역변수로 설정하였음.
// 여러 기능들이 가져올 DOM들을 설정하였음.

/* 댓글쓰는 곳에 내용이 null이 아니면 css가 변경됨 */
commentDone.addEventListener("keydown", function(e) {
    if (commentDone.value.length !== null) {
        submitButtonClick.classList.add("clickbutton") //clickbutton이 변경될 css 클래스
    }
})
// addEventListener로 target을 DOM노드를 준 것. 아래에서도 같은 DOM노드에 다른기능을 추가하였음.

/* 댓글쓴사람명 임시값 */
const superUser = "js_Park"

/* 댓글달기 기능 함수 */
function commentWrite() { 
    let btag = document.createElement("b");
    btag.innerHTML = superUser;    
    let commentViewSpan = document.createElement('span'); 
    let commentText = commentDone.value;       
    commentViewSpan.innerHTML = commentText;
    let result = document.getElementsByClassName("comment-view-div")[0];
    result.appendChild(btag);    
    result.appendChild(commentViewSpan);
    let brtag = document.createElement("br");
    result.appendChild(brtag);  
}
// 기능을 정의해놓고 원하는 DOM노드들에 addEventListener를 할 준비를 했다.

/* 게시 버튼 클릭 시 댓글함수 실행 */
submitButtonClick.addEventListener("click", function() {
    commentWrite();
});

/* 엔터키 눌렸을 때 댓글함수 실행 */
commentDone.addEventListener('keydown', function(e) {    
    if (e.keyCode === 13 ) {
        commentWrite();
    }
})
// 위와 같은 DOM노드에 또 다른 기능을 간단하게 추가한 코드.
// 또한 같은 기능을 하는 함수를 여러 DOM노드 작성하였음.
```
