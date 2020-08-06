## REACT CRA Typescript (OS WINDOW10)  초기세팅하기

### 1. CRA빌드를 이용하여 REACT 작업환경 구성

CRA도 기본 javascript환경외에 typescript 환경도 가능함.

처음 빌드 파일들을 설치하는 명령어로 초기 빌드 구성.

```tsx
//npx create-react-app my-app --template typescript
//or
//내가 선택한 것
yarn create react-app my-app --template typescript
```

\* 만약 기존 javascript로 빌드된 CRA에서 typescript를 사용하고자 한다면 업그레이드 하는 다른 명령어가 있음. 

필요시 구글링 추천드림. 위 명령어는 최초부터 타입스크립트로 빌드를 하기위한 것임



### 2. eslint,prettier 세팅

위에 CRA를 이용한 타입스크립트 빌드환경 구성은 어렵지 않다. 그런데 eslint와 prettier 세팅이 생각보다 잘 안된다. 

\*eslint 말고 typescript를 위한 TSlint 그 외 또다른 javascript lint 툴은 JSHINT 등등 많은 툴이 있으나 타입스크립로 프로젝트들도 eslint많이 하는 추세라는것에 eslint로 세팅하였다.

\*lint가 무엇인지, 또 이런 도구들이 무엇을 의미하는지는 구글링 조금만 더 해보면 자세히 나와있음

\*parser가 무엇인지 등등



아래는 eslint를 airbnb 스타일로 세팅한다는 것


```tsx
//npm install eslint-config-airbnb-typescript --save-dev
//or
//내가 선택한 것
yarn add --dev eslint-config-airbnb-typescript
```
