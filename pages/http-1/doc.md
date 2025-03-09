# 1. https & http

---

## 1.  http란 ?

http는 서버/클라이언트간 데이터를 주고받기 위한 프로토콜이다.

클라이언트에서 request(요청)을 보내면 서버에서는 그에 따른 response를 보내는 구조이다.

http는 **무상태 프로토콜**이라 불리운다.

<aside>
💡

**무상태 프로토콜이란?**

서버에서 클라이언트의 이전 상태를 저장하지 않음을 의미한다. 예로들면

```
Stateful(상태 유지)

고객: 이노트북 얼마인가요?
점원: 100만 원입니다.

고객:2개 구매하겠습니다.
점원: 200만 원입니다. 현금, 카드 중 어느 걸로 구매하시겠습니까?

고객:카드로 구매하겠습니다.
점원: 200만 원 결제 완료되었습니다.
```

이렇게, 서버에서 클라이언트의 이전 말을 기억해야만 작동하는것을 **statsFull(상태 유지)**라 부른다. 그럼, 무상태란 무엇일까?

```
고객: 이노트북 얼마인가요?
점원: 100만 원입니다.

고객:노트북 2개 구매하겠습니다.
점원: 200만 원입니다. 현금, 카드 중 어느 걸로 구매하시겠습니까?

고객:노트북 2개를 카드로 구매하겠습니다.
점원: 200만 원 결제 완료되었습니다.
```

이렇게, 서버에서 클라이언트의 이전 말을 기억하지 않아도, 대화가 가능한것이 무상태**(stateless)**라한다.

이 무상태 와 상태 유지를 어디에서 사용할까? 예로들어 단순한 서비스 소개화면이라면, 무상태 프로토콜을 사용해도 상관없지만, 회원가입과, 로그인등은 상태를 유지한채 사용해야 하기 때문에 이럴떄는 상태 유지 프로토콜을 써야한다. 이 경우엔 실제로 웹사이트의 쿠키나 서버의 세션등을 사용하여 유지한다.

출처:

https://rob-coding.tistory.com/18

[💻평범한 공대생의 개발 노트💻:티스토리]

</aside>

또한, http는 비연결성 프로토콜이라 불리운다.

<aside>
💡

비연결성 프로토콜?

기본적으로 연결을 유지하지 않은 네트워크 모델이다. 이와 반대인 연결 유지 프로토콜은 통신을 위해 한 번 요청을 보내면 후에 요청을 보내지 않아도 계속 클라이언트와 서버가 연결되어있다. 이런 적정치 않은 자원 낭비를 막기 위해, http는 비연결성 프로토콜으로 되어잇다.

</aside>

---

## 2. http 구조

http 메시지는 다음과 같은 구조를 가지고 있다.

> start-line, header, empty line, message body
>

1. start-line

http 요청 메시지에서의 시작 라인은 다음과 같은 request-line으로 이루어져 있다.

> method sp(공백) request-target sp HTTP-version CRUF(개행)
>
- method : HTTP 메서드를 의미한다. GET, POST , PUT, DELETE등이 있다.
- request-target : 말 그대로 요청 대상, 리소스의 경로를 의미한다.
- HTTP-version : 말 그대로

1. header

header-field로 이루어져 있는데, 다음과 같다.

> field-name “:” OWS(띄어쓰기 허용) field-value OWS
>

이 헤더에는 https 메시지 바디의 내용과 크기, 압축, 인증, 요청 클라이언트 등의 정보등이 담겨 있다.

1. message-body

응답 메시지에서의 시작 라인은 다음과 같은 status-line으로 이루어져 있다.

> HTTP-version SP status-code SP reason-pharse CRUF
>
- status-code : https상태 코드를 의미한다. 요청에 대한 성공, 실패 등등.. 여러가지가 있다.
- reason-pharse : 사람이 이해 가능한 짧은 상태 코드 설명 글이다.

---

### 3. 실습

google 웹페이지에 요청 보내서 나오는거 찾아보기~~

> GET /inputtools/images/tia.png HTTP/1.1
Host: [www.gstatic.com](http://www.gstatic.com/)
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:137.0) Gecko/20100101 Firefox/137.0
Accept: image/avif,image/webp,image/png,image/svg+xml,image/*;q=0.8,*/*;q=0.5
Accept-Language: ko-KR,ko;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate, br, zstd
Referer: https://www.google.com/
>

응답 : 이미지