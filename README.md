## react-router-dom
```
구현하고자 하는 애플리케이션은 서버 사이드 렌더링이 아닌 클라이언트 사이드 라우팅은 한 페이지에서만 동작하는 싱글 페이지 애플리케이션 SPA이다.
서버로 어떤 요청도 날리지 않고 모든 라우팅은 클라이언트 코드, 즉 자바스크립트가 해결한다.
http://localhost:3000/login url을 치면 리액트 라우터가 이를 가로채고 url을 해석해 Login 컴포넌트를 렌더링한다.
인터넷이 끊기더라도 Login 페이지를 가져오는 요청은 실행된다. 보편적인 브라우저가 작동하는 방식인 서버사이드 라우팅과는 다르다.
이 프로젝트에서는 클라이언트 사이드 라우팅 라이브러리인 react-router-dom을 사용한다.
```
#### react-router-dom 설치
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/13e76f7d-c00b-462e-acaa-48c2de9e883b)
```
리액트 애플리케이션이 존재하는 경로로 들어가서 react-router-dom을 설치한다.
```
#### Login Component
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/dff8102c-0b7e-4838-82b3-d585687df177)
```
http://localhost:3000/login에서 렌더링할 컴포넌트인 Login 컴포넌트를 작성한다.
```
#### AppRouter Component
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/53b99e0c-b3aa-4706-a0f7-543287920072)
```
localhost:3000/login 경로는 <Route path="login> element={<Login />} />와 같이 컴포넌트를 선언하여 실제 경로를
지정해준다.
<Routes>는 여러 개의 <Route>를 관리하고 실제로 갖아 적합한 <Route>를 찾아주는 컴포넌트이다.
```
#### index.js 수정
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/1385eaf7-7085-4f05-a97e-4ea35751fd1e)
```
가장 처음 렌더링되는 컴포넌트가 AppRouter 컴포넌트가 되도록 수정한다.
```
#### 로그인 페이지 테스팅
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/ae797354-cae6-45ba-aba2-dc28ba1acd40)
```
프론트앤드를 재시작하고 http://localhost:3000/login 페이지로 들어가면 로그엔 페이지 문구가 뜬다면
라우팅이 제대로 동작하는 것을 알 수 있다.
```
#### ApiService: 403 redirect

```

```
## Login 페이지
```
로그인 API 서비스는 /auth/signin 경로였다. 이 경로를 이용해 로그인하는 메서드를 ApiService.js에 작성한다.
로그인 서비스 함수들을 ApiService.js에 작성한다.
```
#### ApiService: signin 함수

```

```
#### Login.js

```

```
#### 수정한 로그인 페이지 테스팅

```

```
#### 로그인 성공
```

```
#### 로그인 성공 시 메인 화면으로 리디렉트 ApiService: signin 함수 수정

```

```
