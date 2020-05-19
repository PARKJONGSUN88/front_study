## 객체, object.. json

#### 1. 객체를 왜 알아야 하느냐.
실제로 DB와 백엔드에서 프론트로 전달해주는 데이터는 객체형태로 되어있는 경우가 많다. 일명 JSON 형태

JSON( JavaScript Object Notation ). 

프론트엔드 개발자라면 이 데이터를 전달받아 사용할 줄 알아야 하느니!



#### 2. 객체란

객체는 값을 배열처럼 많은 value를 가지고 있다.
그러나 배열처럼 순서가 있는것이 아니다.

**배열은 그 안의 값들이 인덱스 값으로 순서를 가지고 있다!**

그러면 객체는 그 값들을 어떻게 찾아가느냐. 그것이 키이다.
객체는 키와 벨류로 이뤄진 집합이다.

```javascript
let myObject = {};
let arr = []; 
```

객체는 {}중괄호로 선언, 표기한다.

배열은 []대괄호임.



```javascript
let jspark = {
	name: "jongsun",
	city: "suwon",
	nuber: 30
};

console.log(jspark);
//{ name: 'jongsun', city: 'suwon', number: 30 }
```

name: "jongsun" 는 프로퍼티이다. 객체안에서 한쌍의 키와 벨류값 세트.



name은 jspark객체의 키 중 하나이다. 

**첫번째 키라고 하진 않겠다. 처음에 선언되었긴 하지만 객체의 값들은 순서가 없기 때문에**



"jongsun"은 name의 키가 가르키는 value값 이다. 즉 실제 인자 값이다.



**객체의 규칙이 있다.**

property의 키 이름은 중복될 수 없다. **value값은 중복 상관없다**

키와 벨류 사이에 :(콜론)으로 구분한다.

property를 추가할 때는 ,(쉼표)를 붙여준다.

value에는 어느 type이나 가능하다(string, number, array, object, function..)





#### 3. 객체를 다루는 법(접근하는 법)

**점표기법(Dot notation)과 괄호표기법(Bracket Notation)**



\2. 대괄호([])를 사용하여, 접근하려는 객체명은 왼쪽에, 프로퍼티명은 쌍따옴표("")와 함께 대괄호 안에 작성합니다.





**1. 점표기법(Dot notation)**

. 마침표(.) 연산자를 사용하며, 접근하려는 객체명은 왼쪽에, 프로퍼티명은 오른쪽에 위치한다.

```javascript
let jspark = {
	name: "jongsun",
	city: "suwon",
	number: "suwon"
};
console.log(jspark.name);//'jongsun'
```



**2. 괄호표기법(Bracket Notation)**

대괄호([])를 사용하여, 접근하려는 객체명은 왼쪽에, 프로퍼티명은 쌍따옴표("")와 함께 대괄호 안에 작성한다.

```javascript
let jspark = {
	name: "jongsun",
	city: "suwon",
	number: "suwon"
};
console.log(jspark["name"]);//'jongsun'
```



두개의 주요한 차이점은 bracket notation을 통해 변수를 통과시킨다.


```javascript
let js = {   
   city: "suwon"
}; //객체선언

let yourHome = "city"; //다른 변수 선언

console.log(js[yourHome]); //'suwon', 변수의 값인 city가 객체의 키값이 된것이다. 
```

이렇게 접근하고 싶은 객체의 키값을 변수를 통해 접근할 수도 있음.

