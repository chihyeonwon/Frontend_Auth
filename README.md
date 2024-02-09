## CORS (Cross-Origin Resource Sharing)

```
독립적으로 존재하는 프런트엔드 애플리케이션(Todo_Frontend)과 백엔드 애플리케이션(Todo_Backend)을
하나씩 개발하였고 이제 두 애플리케이션을 통합해 하나의 기능을 하는 웹 애플리케이션을 완성한다.

프론트엔드에서 백엔드에 API를 호출하는 코드를 짠다.

애플리케이션을 통합하는 과정에서 CORS 문제를 맞닥뜨리게 된다. 이 문제는 백엔드에서 해결해야 한다.
```

#### 백엔드 서버 실행
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/e7c32536-f73d-49e9-98fe-142b4de6861e)
```
이클립스에서 만들어 둔 백엔드 어플리케이션(Todo_Backend)을 실행한다. 여기서 백엔드 서버의 도메인은 localhost:8080이다.
```
#### App.js: API를 이용해 리스트 초기화
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/f347447b-a1a9-4060-8706-4381521b9cc6)
```
fetch 함수를 사용해서 todo API를 사용해서 리스트를 초기화한다. 
```
#### CORS 에러 
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/72ac81e2-b048-413f-a6ed-ca581b281290)
```
localhost:3000으로 들어가 개발자 툴의 콘솔 창을 열어보면 CORS 에러를 확인할 수 있다.

보안을 위한 CORS 헤더 Policy를 위반했기 때문이다. 처음 리소스를 제공한 도메인(Origin)이 현재 요청하려는 도메인과
다르므로 요청이 거절된다.

Origin(localhost:3000 프론트엔드단)에서 백엔드 서버 도메인으로 요청 != (localhost:8080 백엔드단 서버)

CORS를 가능하게 하기 위해선 백엔드에서 CORS 방침 설정을 해줘야 한다.
```
#### WebMvcConfig.java
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/1998abff-97a1-490a-a7e3-fb1177c1b237)
```
스프링부트 어플리케이션 프로젝트로 돌아가서 config 패키지 아래에 WebMvcConfig 클래스를 작성한다.
WebMvcConfigurer 인터페이스를 구현한다. addCorsMapping에서 모든 경로에 대해 Origin이 http://localhost:3000인 경우
GET, POST, PUT, PATCH, DELETE, OPTIONS 메서드를 이용한 요청을 허용한다.

또한 모든 헤더와 인증에 관한 정보 Credential도 허용한다.
```
#### CORS 에러 삭제
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/5d1c6226-7a18-48b5-814e-11139e25df0e)
```
백엔드 어플리케이션을 수정한 후 재실행하면 더 이상 CORS 에러가 나지 않는 것을 확인할 수 있다.
```
## Effect Hook을 이용한 Todo 리스트 초기화
#### Todo API 무한루프
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/16c9d233-f4aa-4d3a-8486-10900c2ed28f)
```
CORS로 인한 에러메시지는 사라졌지만 네트워크 탭을 열어보면 todo가 끝없이 나열된 것을 확인할 수 있다.
이는 fetch 함수를 사용한 API 호출이 비동기 호출이여서, 즉 API 호출한 후 응답이 올 때까지 기다리지 않는다.
fetch함수의 then 함수 체인은 setItem을 부르면 item의 상태가 새로초기화되고 상태가 바뀌었음을 리액트는 재렌더링을 위해
App() 함수를 호출하고 다시 API 호출 -> then의 setItem -> App() -> API -> setItem -> App() 무한 루프에 빠지게 된다.

이를 방지해주는 것이 리액트 훅 중 Effect 훅인 useEffect() 함수를 이용하면 무한 루프에 빠지지 않고도 처음 리스트를 불러오는
부분을 구현할 수 있다.
```
#### useEffect로 Todo API 호출
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/5b629e11-e414-469c-9c28-d5ffa763c1f3)
```
useEffect는 함수와 배열을 인자로 받는다.
fetch 함수 호출 부분을 useEffect함수 안으로 넣고, 빈 배열을 넣어줬다.

첫 렌더링 이후에 배열 안의 오브젝트의 값이 변할 때마다 콜백 함수를 부른다.
```
#### useEffect를 이용하여 렌더링 무한 루프 탈출
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/df56950a-fb57-43a8-b27b-9a55a5e4ee97)
```
useEffect 함수를 사용하여 첫 번째 인자로 넘겨준 API를 가져오는 fetch함수를 호출한 후 빈 배열을 넘겨줘서
리액트 렌더링 무한 루프에 빠지는 것을 방지하였다. 
```
#### Fetch API 사용법
```
Fetch 함수는 url을 매개변수로 받거나 url, options를 매개변수로 받을 수 있다. 또 Promise 오브젝트를 반환한다.
메서드를 명시하고 싶은 경우나 헤더나 바디를 함께 보내야 할 경우에는 두 번째 매개변수에 요청에 대한 정보가 담긴
오브젝트, options를 넘겨준다.
```
#### api-config.js
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/2a39a52a-4c63-4fc1-86f6-96194e4fec54)
```
브라우저의 도메인이 localhost인 경우 로컬 호스트에서 동작하는 백엔드 애플리케이션을 사용하도록 url을 설정한다.
```
#### ApiService.js
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/75b60523-d1a0-4ade-9282-b0b56b3452a0)
```
백엔드로 요청을 보낼 때 사용하기 위한 유틸리티 함수인 call 함수를 작성한다.
```
#### App.js: ApiService 사용
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/475bf856-2919-498a-91b3-6a88f160d42c)
```
기존 App.js의 코드에서 ApiService의 call 함수를 사용하여 localhost:8080/todo 로 GET, POST, DELETE 요청을 보냈을 때
각각의 요청에 대한 응답을 불러오도록 한다. 프론트엔드 리액트에서 생성한 json 형식의 item 을 문자열형식으로 바꿔서
응답바디로 넣는다.
```
#### 백엔드의 데이터베이스에서 Todo 리스트 가져오기 테스트
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/6f1a6360-8e73-4091-91ad-83ead0a67ae4)
```
브라우저를 새로고침한 후 Todo 아이템을 추가한 뒤 새로고침하여도 사라지지 않는다. 또는 프론트엔드 애플리케이션을
완전히 종료했다가 다시 켜도 사라지지 않는다.
```
## Todo Update 수정
#### App.js: editItem 함수 수정
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/9eb90be9-a7c8-450e-9869-22ec6210001b)
```
Server API를 이용해서 서버 데이터를 업데이트 한후 변경된 내용을 다시 출력하는 두 가지 작업이 필요하다.

Todo.js에서 editItem을 사용할 때 item을 매개변수로 넘겨줘야 한다.
```
#### Todo.js: editItem()에 item을 매개변수로 넘기기
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/5a459c9b-9f93-400d-a510-f0d3601ddd24)
![image](https://github.com/chihyeonwon/Frontend_Backend/assets/58906858/2df5069e-1442-49d6-9e6e-f5ea7122bed4)
```
editEventHandler()에서는 프론트엔드에서의 item의 값만 업데이트하고 HTTP 요청은 보내지 않도록 수정한다.
이후 사용자가 엔터키를 누르는 순간 실행되는 turnOnReadOnly()에서 HTTP 요청을 보내는 editItem()을 실행한다.
```

