## react 설치 및 실행

#### 1. 설치
 1. react는 npm으로 설치된다. 

   

2. npm(node package manager)이니 node.js가 필요하다.
   node.js는 js(브라우저,인터프리터 언어)를 서버(터미널환경)에서 사용할 수 있게한 프로그램.

   

3. node.js, npm이 설치하고 정살적으로 됬을 경우

```terminal
$ node -v
v14.2.0
  
$ npm -v
v6.14.4
```

이라고 버전 정보가 출력된다.



4. cra(create-react-app)을 활용해서 할 예정.

​      react앱을 만들때 기본적으로 필요한 것들을 제공해주는 npm의 패키지 라고 생각하면 됨.
```terminal
$ npm install -g create-react-app 
```

​    -g는 global옵션으로 create-react-app를 어디서든 쓸수있게 패스지정하는것이라고 생각하면 된다.



5. 폴더 준비 및 create-react-app화 작업.

   우선 workspace로 사용할 폴더를 준비하고 해당 폴더에서 npm의 cra패키지를 이용한다
```terminal
$ cd 해당폴더
$ create-react-app .
```

해당 폴더로 이동한뒤 **create-react-app .** 로 "그 폴더를 cra로 쓰겠다고 명령"한다.



#### 2. 실행

1.  react폴더에서 npm run start를 하여 서버를 실행할 수 있다.

2.  배포시에는 npm run build임.

    build는 불필요한 리액트파일들을 빼고 실제로 필요한 것들만 용량을 줄여서 올라가게 하기 위해 있는 배포모드다. 개발중 사용하는 것이 아니라 최종 배포전에 압축해서 올리는 것이라고 생각하면 됨.