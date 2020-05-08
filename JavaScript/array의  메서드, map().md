## array의  메서드, map()

map 메서드는 자바스크립트 배열의 내장 메서드인데 배열안의 값들을 반복해서 리턴해준다.

map메서드 안의 callback 함수에서 return한 값으로 매요소(foreach같은)를 수정하여 리턴해준다.

map 메서드의 return값은 수정된 값으로 다시 생성된 새로운 배열이다.



```javascript
let arr = [1, 2, 3];
console.log(arr); //[1, 2, 3]

let newArr = arr.map(
    function(e) { //map메서드의 콜백함수
	return e + 3;
});
console.log(newArr); //[4, 5, 6]
```



arr의 요소들이 map메서드의 콜백함수에서 인자에 3을 더하여 반환하라는 함수의 결과 후

새로운 변수 newArr에 담김.





예제2)

```javascript
let arrHangle = ["가", "니", "다"];
console.log(arrHangle); //["가", "나", "다"]

arrHangle = arrHangle.map(function(){
	return  "한글"
});
console.log(arrHangle);//["한글", "한글", "한글"]

```

이번엔 arrHangle 이라는 변수에 배열로 "가", "나", "다" 라는 3개의 인자를 담았다.

그리고 다시 이 arrHangle변수에 맵메서드를 이용해서 새로운 값을 집어넣었는데

메서드 안의 콜백함수에서는 파라미터가 없이 그대로 "한글"이라는 인자값을 리턴하라고 했더니

foreach와 같이 arrHangle의 모든 요소가 "한글"로 바뀌었다.


