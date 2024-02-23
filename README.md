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
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/12a81c1b-d198-4adf-baf7-cd56253dfab6)
```
브라우저의 개발자 도구에서 콘솔에 다음 코드를 작성하여 로컬 스토리지에 아이템을 저장하고 원하는 아이템을 가져왔다.
```
#### 스토리지 탭
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/e2d003ea-a2e7-4fa2-aba7-28fdaa605a47)
```
Application의 Local Storage를 확인할 수 있다.
주소 경로마다 따로 저장된다. 따라서 다른 도메인의 자바스크립트는 다른 도메인의 로컬 스토리지를 읽지는 못한다. 
```
#### 액세스 코드 저장
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/7f26c757-cc23-45cf-960a-c40cb61afa78)
```
로그인 시 받은 토큰을 로컬 스토리지에 저장하기 위해서 ApiService의 signin 함수를 다음과 같이 수정한다.
```
#### ApiService.js: 엑세스 토큰 헤더에 추가

```javasciprt
export function call(api, method, request) {
  let headers = new Headers({
    "Content-Type": "application/json",
  });

  // 로컬 스토리지에서 ACCESS TOKEN 가져오기
  const accessToken = localStorage.getItem("ACCESS_TOKEN");
  if (accessToken && accessToken !== null) {
    headers.append("Authorization", "Bearer " + accessToken);
  }

  let options = {
    headers: headers,
    url: API_BASE_URL + api,
    method: method,
  };
  if (request) {
    // GET method
    options.body = JSON.stringify(request);
  }
  return fetch(options.url, options)
    .then(response => {
      if (response.status === 200) {
        return response.json();
      } else if (response.status === 403) {
        window.location.href = "/login"; // redirect
      } else {
        new Error(response);
      }
    })
    .catch(error => {
      console.log("http error");
      console.log(error);
    });
}
```
```
모든 API의 헤더에 액세스 토큰을 추가하는 부분을 구현한다.
call에 토큰이 존재하는 경우 헤더에 추가하는 로직을 작성한다.
```
#### 로그인 성공 시 메인화면으로 라우팅
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/f8771255-a3e3-4272-b52d-eb3d0e06d7cf)
```
API 콜을 할 때마다 로컬 스토리지에서 토큰을 가져와서 헤더에 포함시킨다. 올바른 토큰이므로 백엔드는 인증에 성공하고
메인 화면으로 정상적으로 라우팅될 수 있게 되었다.
```
## 로그아웃과 글리치 해결

#### 로그아웃 서비스
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/48dab3a8-3ad8-4370-88d8-eb83e1009341)
```
ApiService에 signout 함수를 작성한다. 로컬스토리지에 있는 액세스 토큰을 모두 null 값으로 만드는 로직이다.
```
#### App 컴포넌트에 네비게이션 바 추가
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/5f6481ef-f30c-4583-aa9c-3cd89cffd1a5)
```
material UI에서 제공하는 AppBar와 Toolbar를 사용하여 네비게이션 바 컴포넌트를 생성하고 리스트 렌더링 위에
이 컴포넌트를 추가한다.
```
#### 네비게이션 바 테스팅
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/137ea3fd-e23c-4380-8857-66c86a9789e6)
```
네비게이션 바의 맨 오른쪽에 로그아웃 버튼에 signout 함수를 연결하여 클릭하면 로그아웃이 되도록 기능을 구현하였다.
```
#### 로그아웃 기능 구현
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/8e54d4c0-3672-4633-bfb0-3efc3ee5cc7c)

## UI 글리치 문제 해결
```
Todo 리스트 페이지에 접속한 후 로그인 페이지로 라우팅하기까지 걸리는 시간 때문이다.
이 시간은 백엔드 서버에 todo를 요청하고 결과를 받아 확인하는 데 걸리는 시간이다.
로그아웃 상태에서 아무것도 할 수 없지만 UI가 이렇게 오락가락하는 것은 사용성 측면에서 좋지 않다.
이를 방지하기 위해서 백엔드에서 todo 리스트를 받아오기 전까지는 로딩 중이라는 메시지를 띄우도록 한다.
```
#### App.js 로딩중 로직 추가
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/9df96e2f-ef4d-41db-88a7-80603c403230)
```
로딩 중이 아닐 때는 todoListPage 컴포넌트를 렌더링하고 todo 백엔드 서버에 요청을 보내고 응답을 받아오는 중인
로딩 중인 상태일 때는 로딩중...메시지가 보여지는 content 컴포넌트를 렌더링하도록 로직을 작성했다.
```
#### 로딩중 화면 테스트
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/c1262bba-0c1c-45e4-891d-8c354413d69b)
```
로그인하지 않은 상태에서 localhost:3000에 접근하면 로딩중..이라는 화면이 뜨다가 로그인 화면으로 전환되는 것을
알 수 있다.
```
## 계정 생성 페이지

#### ApiService: singup 함수 추가
![image](https://github.com/chihyeonwon/Frontend_Auth/assets/58906858/5b633cc3-522a-46e7-95db-cb65f9d83c7a)
```
ApiService에 signup 메서드를 추가한다. 이 메서드를 이용해서 백엔드에 signup 요청을 보낸다.
```
#### 계정 생성 페이지

```

```
#### AppRouter: SingUp 라우트 추가

```

```
#### 로그인 컴포넌트 수정

```

```
#### 계정 생성 페이지 테스트

```

```
