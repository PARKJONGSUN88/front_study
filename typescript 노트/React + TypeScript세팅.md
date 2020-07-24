## React + TypeScript 세팅

리엑트 + 타입스크립트 조합으로 프로젝트를 진행할 때 사용한 세팅.

리엑트는 CRA로 타입스크립트버전으로 시작하였으며 airbnb eslint 스타일을 사용했다.



```
//vscode settings.json

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

```
//프로젝트 root/.eslintrc

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

```
//프로젝트 root/.prettierrc 

{
  "singleQuote": true,
  "semi": true,
  "useTabs": false,
  "tabWidth": 2,
  "trailingComma": "all",
  "printWidth": 80
}
```

```
//프로젝트 root/tsconfig.json

{
  "compilerOptions": {
    "target": "es5",
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react"
  },
  "include": [
    "src"
  ]
}
```

```
//package.json

{
  "name": "my-app",
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
    "@types/react-icons": "^3.0.0",
    "@types/react-router-dom": "^5.1.5",
    "@types/styled-components": "^5.1.1",
    "react": "^16.13.1",
    "react-dom": "^16.13.1",
    "react-router-dom": "^5.2.0",
    "react-scripts": "3.4.1",
    "styled-components": "^5.1.1",
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
    "@typescript-eslint/eslint-plugin": "^3.4.0",
    "@typescript-eslint/parser": "^3.4.0",
    "eslint": "^6.6.0",
    "eslint-config-airbnb-typescript": "^8.0.2",
    "eslint-config-prettier": "^6.11.0",
    "eslint-plugin-prettier": "^3.1.4",
    "prettier": "^2.0.5"
  }
}
```

