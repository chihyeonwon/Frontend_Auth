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
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/6d33adcc-a40a-40a6-b2fb-f641e8c7e475)
```
ApiService의 call 메서드는 fetch 함수를 부른다. fetch를 이용하면 API 콜을 한 후, .then을 이용해 HTTP 응답을 받아온다.
이때 받아온 HTTP의 응답의 Status 값이 200이라면 정상, 403이라면 인증에 실패한 것이다. 403인 경우 Login 화면으로 리디렉트하는
로직을 작성해주었다.
```
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/ef654f76-40a7-4ec7-996a-e8bcabdf3598)
```
http://localhost:3000으로 접근하면 login 페이지로 리디렉트되는 것을 확인할 수 있다.
```
#### Login.js
```javascript
const Login = () => {
  const handleSubmit = event => {
    event.preventDefault();
    const data = new FormData(event.target);
    const username = data.get("username");
    const password = data.get("password");
    // ApiService의 signin 메서드를 사용 해 로그인.
    signin({ username: username, password: password });
  };

  return (
    <Container component='main' maxWidth='xs' style={{ marginTop: "8%" }}>
      <Grid container spacing={2}>
        <Grid item xs={12}>
          <Typography component='h1' variant='h5'>
            로그인
          </Typography>
        </Grid>
      </Grid>
      <form noValidate onSubmit={handleSubmit}>
        {" "}
        {/* submit 버튼을 누르면 handleSubmit이 실행됨. */}
        <Grid container spacing={2}>
          <Grid item xs={12}>
            <TextField
              variant='outlined'
              required
              fullWidth
              id='username'
              label='아이디'
              name='username'
              autoComplete='username'
            />
          </Grid>
          <Grid item xs={12}>
            <TextField
              variant='outlined'
              required
              fullWidth
              name='password'
              label='패스워드'
              type='password'
              id='password'
              autoComplete='current-password'
            />
          </Grid>
          <Grid item xs={12}>
            <Button type='submit' fullWidth variant='contained' color='primary'>
              로그인
            </Button>
          </Grid>
        </Grid>
      </form>
    </Container>
  );
};
```
```
로그인 컴포넌트는 이메일과 패스워드를 받는 인풋 필드, 로그인 필드로 이루어져 있다.
사용자가 이메일과 패스워드를 입력한 후 로그인 버튼을 누르면 작성한 ApiService의 signi 메서드를 이용해서
백엔드의 /auth/singin으로 요청이 전달된다.
```
#### 수정한 로그인 페이지 테스팅
#### Postman으로 유저 생성
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/1b52dbda-6b9c-4d51-848d-42971ee4e385)
#### 생성한 아이디, 비밀번호로 로그인 페이지에서 로그인 시도
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/a9fdbf57-c5da-4510-b8ff-3a122825994b)
#### 로그인 성공 (Token alert 메시지 반환)
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/6aa19a11-b357-4b3c-88c5-68bf1b8c69b5)
```
POSTMAN으로 새 유저를ㄹ 만든 후 login 페이지에서 로그인을 시도하여 로그인에 성공하면 alert 메시지에
토큰이 기록되는 것을 확인할 수 있다.
```
## 로그인 성공
#### 로그인 성공 시 메인 화면으로 리디렉트 ApiService: signin 함수 수정
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/e7f6311c-fea2-4f31-bec2-027d7dd4c327)
```
로그인에 성공한 경우에는 Todo 리스트가 있는 화면으로 돌아가야 한다. 따라서 토큰이 존재하는 경우 Todo 리스트 화면인
localhost:3000/으로 돌아가는 로직을 작성해야 한다. ApiService의 signin 함수를 수정한다.
```

## 로컬 스토리지를 이용한 액세스 토큰 관리

#### 로컬 스토리지 실습

```

```
#### 액세스 코드 저장

```

```
#### ApiService.js: 엑세스 토큰 헤더에 추가

```

```
