## Sass

css와 같은 스타일을 파일이나 css에서 조금 더 확장된 기능을 추가한다고 생각할 수 있다.



### 변수

자주 사용되거나 value가 복잡하다던지 등을 변수로 저장하여 원하는 곳에서 하나의 값으로 사용할 수 있다.

```sass
$mainColor : "blue";

div {
   color:$mainColor;
}
```



### 네스팅(중첩)

스타일도 스크립트나 html처럼 부모자식관계로 묶어 관리할 수 있다.  

이 경우 css로 할때처럼 불필요한 class네임을 사용하지 않을 수 있다.

```sass
.commentScore {
  width: 15em;
  .tipWrap {
    .tip {
      padding: 1em 0;
      margin-left: 0em;
      width: 15em;
   }
  }
}
```



### &(상위선택자)

네스팅에서 ```&``` 는 부모를 참조하여 사용되며 만약 ```& > 태그 ```를 할 경우 자식에게 전달할 수 있다.

```sass
.list {
  li {
    &:last-child {
      margin-right: 0;
    }
  }
}
```

```sass
.commentScore {
  width: 15em;
  & > ul >li {
  	color:"red";
  }  
  .tip {
  	margin-left: 0em;
  	width: 15em;
  }  
}
```



