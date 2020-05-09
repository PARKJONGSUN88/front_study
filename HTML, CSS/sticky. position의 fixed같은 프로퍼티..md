## sticky. position의 fixed같은 프로퍼티.

div를 고정시키고자 한다면 자주 쓰던 position:fixed가 있다.

하지만 fixed는 뷰포트를 기준으로 하기에 어떠한 경우 불편할 경우가 있다.

맨위에 있는 nav바가 아니라 sidebar나 중간 content에 있는 어떠한 div요소라던지... 

이럴 때 쓰는게 새로나온 CSS의 프로퍼티인 **sticky**이다.

 

flex를 하다보니 fixed로 하기에 맞지 않아 sticky를 적용한 내 코드 

**flex로 div를 배치하다가 보니 fix로는 해결이 안되었다...**

```css
.main-right {
    position:sticky; //스티키 포지션을 해라
    top:5em;         //위에서 5em띄우고 고정이다. 스크롤 할때 보여진다.
    display:flex; 
    align-items: center;
    justify-content:center;
    width: 20em;
    height: 40em;
    margin-left: 1em;  
}
```

순수 css만으로 fixed와 같은 효과를 낼 수 있다!!!

fixed는 부모요소의 relative, fixed를 기준으로 하지만 sticky는 그런거 없이 

**그 요소만 딱! 스티커처럼 달라붙어 고정된다~~**





적용하는 것은 위의 코드처럼 position속성의 프로퍼티로써 sticky를 쓰고

그리고 스크롤 할 시 기준으로 해야되기떄문에 보통의 경우 top:0px; 등을 하면 되겠다.



**원래 위 기능을 구현하려면 자바스크립트로 스크롤할때마다 해당 엘리먼트의 offset 좌표와 스크롤위치를 비교해서 해야되는 것이라 그런지 top기준으로 써야된다.**



그런데 아직 나온지 얼마안되서인지 브라우저 지원범위가 상당히 작다. 

크롬은 거의 되는데 IE11에서조차 지원을 안한다고 하니..