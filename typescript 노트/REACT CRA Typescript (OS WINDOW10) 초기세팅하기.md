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



### 3. 각종 세팅

#### VS code 세팅은 그대로

```tsx
//settings.json

{
  "terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
  "python.pythonPath": "C:\\Program Files\\Python37\\python.exe",
  "editor.suggestSelection": "first",
  "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
  "editor.tabSize": 2,
  "editor.detectIndentation": false,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },  
  "files.autoSave": "afterDelay",
  "workbench.iconTheme": "vscode-icons",
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "editor.formatOnSave": true,
  "eslint.autoFixOnSave": true
}
```

#### eslintrc 세팅 

```tsx
//project root/.eslintrc

{
  "parser": "@typescript-eslint/parser",
  "extends": [
    "plugin:prettier/recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended",
    "prettier/@typescript-eslint"   
  ],
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "rules": {
    "rules": {
      "prettier/prettier": [
        "error",
        {
          "endOfLine": "auto"
        }
      ]
    }
  },
  "settings": {
    "react": {
      "version": "detect"
    }
  },
  "ignorePatterns": ["*.config.js"]
}
```

#### prettier 세팅

```tsx
//project root/.prettierrc

{
  "singleQuote": true,
  "semi": true,
  "useTabs": false,
  "tabWidth": 2,
  "trailingComma": "all",
  "printWidth": 80
}
```
#### package.json 세팅

```tsx
//package.json // eslint버전이 안맞으면 에러남

{
  "name": "test3",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^4.2.4",
    "@testing-library/react": "^9.3.2",
    "@testing-library/user-event": "^7.1.2",
    "@types/jest": "^24.0.0",
    "@types/node": "^12.0.0",
    "@types/react": "^16.9.0",
    "@types/react-dom": "^16.9.0",
    "react": "^16.13.1",
    "react-dom": "^16.13.1",
    "react-scripts": "3.4.1",
    "typescript": "~3.7.2"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "devDependencies": {
    "eslint-config-airbnb-typescript": "^8.0.2",
    "@typescript-eslint/eslint-plugin": "^3.4.0",
    "@typescript-eslint/parser": "^3.4.0",
    "eslint": "^6.6.0",
    "eslint-config-prettier": "^6.11.0",
    "eslint-plugin-prettier": "^3.1.4",
    "prettier": "^2.0.5"
  }
}
```