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



