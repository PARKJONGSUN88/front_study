## 빈스트링, array.filter tip

```javascript
let arr = [
  { "id": 1, "name": "Leanne Graham", },
  { "id": 2, "name": "Ervin Howell", },
  { "id": 3, "name": "Clementine Bauch", }
]

let userInput = "";
let pickme = arr.filter(item => item.name.includes(userInput))
욕
console.log(pickme)
```

이렇게 했을때 결과는 filter에 의해 ```userInput```이 ""이기에 아무것도 안나올 것이라 생각될 수 있다.

그러나 빈스트링과 공백은 다르다. 빈스트링은 모든 스트링을 포함한 것과 같은것으로 

이 결과는 ```arr```안의 모든 요소를 반영한다.
