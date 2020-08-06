## font 설치하는 법

#### 1. 파일 다운로드

먼저 원하는 폰트를 다운받아야 한다.  웹에서 사용중인 것을 다운받고 싶을 땐 해당 웹페이지에서
개발자도구로 들어가서 네트워크탭에서 새로고침 후 나오는 font탭을 보면 알 수 있다.



#### 2. react에 적용할 위치

src\styles\fonts\

에 해당 woff 나 woff2 파일을 집어넣는다. 



#### 3. css에 Add시키기

```jsx
@font-face {
  font-family: Buri;
  src: url(./fonts/Arita-buriM-subset.woff);
}
```
라고 글로벌하게 선언해줬다. 해당 css파일에 해도 되지만 common.css에 하여 어디서든 사용할 수 있게 하였다.




#### 4. 적용시키기

```jsx
 div {
 	font-family:"Buri"
 }
```

원하는 곳에서 css를 적용하여 사용한다!

