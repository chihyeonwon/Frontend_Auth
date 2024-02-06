## 기술 스택
- Node.js, NPM version 16.14.2 LTS
- SPA
- React.js
- material-ui
- Visual Studio Code

#### NPM 설치
[node.js 설치](https://nodejs.org/en/blog/release/v16.14.2)    
#### npm version 확인
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/87fb6473-ac15-4340-b1aa-736519822f76)
```
NPM(Node Pacakage Manager)는 node.js의 패키지 관리 시스템이다.
NPM은 node.js를 설치하면 함께 설치된다.
```
#### node 프로젝트 초기화
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/6d74ed65-7a98-4a8e-815f-e64dc593167e)
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/fc187aa7-e42c-41cf-935b-0b7d04ef47c1)
```
$ npm init 명령어를 이용해서 node 프로젝트를 초기화하면 패키지 이름, 버전 등 기본적인 정보를 입력해야 한다.
이 정보를 입력하면 package.json 파일을 생성하는 데 이 파일에는 프로젝트의 메타데이터가 들어간다.
```
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/0e7b1711-1c0d-470f-892f-a8fed3d3ae6b)
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/57f143f0-208d-4832-bca6-586e341abc5d)
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/dd5f33a9-3dc4-4813-a8e8-bf3394282809)

```
$ npm install react 명령어를 이용해서 react를 설치한다면 해당 패키지는 node_modules 아래에 설치되
package.json의 dependencies에 추가된 라이브러리는 이후 프로덕션 배포에 사용된다.

react 프로젝트 생성 시 npm 대신 npx를 사용한다. npm은 일일이 설정해야 하는 부분이 많기 때문이다.
```
## 프론트엔드 애플리케이션 생성
#### npx crate-react-app
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/a87f46c1-53fa-414a-bfd9-90df0acbad2f)
#### react 애플리케이션 생성 로그
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/1b5d0173-da69-474a-80ca-aa13b44c485f)
```
react-workspace 폴더를 만들고 npx를 이용하여 react 애플리케이션을 생성한다.
```
#### react 애플리케이션 실행
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/df5829d6-2750-4077-be61-b01d404f9996)
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/0481e44e-1e58-4f54-a899-f71f68232bf4)
```
생성된 todo-react-app 폴더로 가서 npm start 명령어를 실행한다.
localhost:3000 포트에서 실행되고 있고 이 경로로 들어가면 애플리케이션을 확인할 수 있다.
```
## Visual Studio Code 개발환경설정
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/11e70120-e33d-418b-9e9b-c4afdc887676)
```
비쥬얼스튜디오 코드를 열고 폴더-작업영역에 폴더 추가를 눌러서 todo-react-app을 추가한다.
작업영역을 todo-react-app-ws라고 저장한다.
```
#### package.json 디펜던시 수정
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/f9a303e9-8815-4d11-a5e7-048ce3df46c4)
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/a3f72c3b-0dd9-4f76-9599-b3ee90db43db)
```
package.json 디펜던시를 수정하고 node_modules와 package-lock.json 를 삭제한다.

node_modules를 삭제하는 이유는 package.json에 명시된 패키지의 새 버전을 설치하기 위함이고
package-lock.json은 node_moduels의 버전을 고정하기 위한 파일이므로 npm start를 실행하여새로운 디펜던시를 설치한다.
```
#### 새로운 디펜던시 설치
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/f6211120-a848-4a0b-ba6f-57296358f07a)
```
npm ERR! code ERESOLVE
npm ERR! ERESOLVE unable to resolve dependency tree

$ npm install dependency 버전 오류가 발생했지만 기존버전 무시하고 설치했다.($ npm install --force)

새로이 node_modules 폴더와 package-lock.json 파일이 생성되었다.
```
#### material-ui 패키지 설치
[material-ui 공식 사이트](https://material-ui.com)
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/4ec81177-14f4-446e-9df4-1e79655d1d1b)
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/61b959f9-3c66-4945-9243-8c38be4157ae)
```
프론트엔드 애플리케이션을 개발하기 위해 material-ui 패키지를 사용한다.
material-ui 관련한 코어 패키지와 emotion에 관련된 패키지를 설치한다.
```
#### Todo 컴포넌트 생성
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/6a5a809d-2234-4188-946e-1d954b184649)
```
Todo 컴포넌트는 간단한 checkbox와 label을 렌더링하는 컴포넌트이다.
```
#### App 컴포넌트에서 Todo 컴포넌트 사용
![image](https://github.com/wonchihyeon/Todo_Frontend/assets/58906858/705d84dc-c89f-4fda-91d8-bb569987af6c)
```
현재 index.js에는 App 컴포넌트가 렌더링되고 있으므로 App 컴포넌트에서 Todo 컴포넌트를 import 하여 사용한다.
```
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/f5ba7264-bc4e-499c-8a6b-f11ef41b9781)
#### Todo 컴포넌트 두 개 사용
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/9837f893-adeb-4aba-ac01-e3b452d7f817)
```
Todo 컴포넌트를 두 번 추가 해준다. JSX도 원하는 컴포넌트를 나열해 원하는 만큼 컴포넌트를 재사용할 수 있다.
```
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/ecba75a1-8fc5-489b-877c-77ce18f30bbf)
#### Todo에 상태 매개변수 전달
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/ae731cea-8718-4774-8573-dfe271ff70dd)
```
useState를 사용해서 매개변수(props.item)에 담겨있는 item을 넘겨받는다.
```
#### App.js에서 Todo로 item 전달
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/c932cd8a-4f27-4129-924d-a29237de4669)
```
useState의 매개변수로 item을 작성하여 Todo 함수로 넘겨준다.
```
#### 렌더링한 결과
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/96af6558-2c25-447c-a400-9cc9b5670dfc)
#### Todo 아이템 리스트 렌더링
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/f6e17055-d5a7-412d-94ec-923b7a6ca0a0)
```
배열에 담긴 Todo 아이템들을 렌더링하기 위해 App.js 코드를 수정한다.
```
#### Todo 리스트 렌더링 
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/34bbc517-ee9f-4be0-a4b4-d8b5a809ca1e)

#### material-ui를 이용한 Todo 컴포넌트 디자인
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/1a9fda38-0c4f-4e0d-a1bc-9781e945c583)
```
material-ui 패키지를 이용해 UI를 변경한다. ListItem, ListItemText, InputBase, CheckBox 등의 컴포넌트를 이용해
복잡한 CSS를 사용하지 않고도 UI를 개선할 수 있다.
```
#### material-ui를 이용한 App 컴포넌트 디자인
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/fdab3905-308d-47e4-ab0f-355590eedf3f)
```
App.js에서는 material-ui 패키지의 List와 Paper를 사용하여 ui를 디자인하였다.
```
#### material ui를 이용해 수정한 화면
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/e4600f2c-abe1-42ad-9632-2cdaa332494e)

## Todo 추가
#### AddTodo.js
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/93fffb11-feb3-4b6a-98e6-06b53264ddec)
```
Grid, TextField, Button을 이용해 사용자의 입력을 받을 인풋 필드와 버튼을 생성한다.
```
#### App.js: AddTodo 추가
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/3bfaf5ff-9937-4922-a51a-e584306d5841)
```
AddTodo로 생성한 UI를 화면에 올리기 위해 App.js에 AddTodo 컴포넌트를 추가한다.
```
#### AddTodo UI 테스팅
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/53451cfa-e267-42b0-8817-66c3ee8c5149)
#### AddTodo.js: onInputChange 함수 작성
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/5d55e653-bac8-41cd-8617-328ea33dd173)
```
키보드를 두드릴 때마다 사건 e가 발생하고 현재 화면의 인풋필드에 입력된 글자들이 담겨 있는 e.target.value를
item의 title로 지정한 후 setItem을 통해 item을 새로 업데이트한다.
TextField에 사용자 입력이 들어올 때마다 onInputChange 함수가 실행된다.
```
#### onInputChange 함수 테스팅
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/34fcca56-033f-4fce-bf8a-d6d4ddae5316)
```
키보드 입력 시 onInputChange 함수가 실행되는 것을 확인할 수 있다.
```
#### App.js: addItem 함수 추가
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/e2c95fd0-9340-422b-a807-da2c355509eb)
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/8d89beab-28d9-46ab-b11d-41310676be48)
```
App 컴포넌트에 addItem 함수를 추가하고 이 함수를 AddTodo의 프로퍼티로 넘겨서 AddTodo에서 사용한다.
```
#### AddTodo.js: addItem 함수 사용
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/fed8c5ed-e282-4222-b21c-8b77ec5e2d5b)
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/58859817-5226-431c-9791-f70de1fa3d0e)
```
AddTodo 컴포넌트에서 App.js의 addItem 함수를 props로 넘겨받아서 onButtonClick 함수를 작성한다.
버튼 클릭 시 onButtonClick이 실행되도록 한다.
```
#### onButtonClick 함수 테스팅
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/d00a3856-7b26-4780-aba1-d6cf73862d87)
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/6bad36d4-ba5f-4c5f-9753-aadc1e624f61)
#### AddTodo.js: enterKeyEventHandler 작성
![image](https://github.com/chihyeonwon/Todo_Frontend/assets/58906858/6c9c2924-8001-4af9-b376-310758db4cfc)
```
Enter 키로 인해 이벤트가 발생하는 경우 onButtonClick() 함수가 실행되도록 엔터키 처리를 위한 핸들러를 작성한다.
```


