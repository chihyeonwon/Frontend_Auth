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

```

```
#### AppRouter Component

```

```
#### index.js 수정

```

```
#### ApiService: 403 redirect

```

```
## Login
