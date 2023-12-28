## **🟦 섹션 3. 모든 것이 HTTP**

### **⬛ 1. 모든 것이 HTTP**

**◼️ HTTP (HyperText Transfer Protocol)**

- 문서 간의 링크를 통해서 하이퍼테스트 문서를 통해 연결하는 프로토콜
- **HTTP 메시지에 ‘모든 것’을 담아서 전송이 가능**하다.
- HTTP 프로토콜에는 HTML, TEXT, IMAGE, 음성, 영상, 파일, JSON, XML (API) 등 거의 모든 형태의 데이터를 담아서 전송이 가능하다.
- 서버 간에 데이터를 주고 받을 때에도 대부분 HTTP 사용한다.

**◼️ HTTP 역사** 

- HTTP/0.9 1991년: GET 메서드만 지원, HTTP 헤더X
- HTTP/1.0 1996년: 메서드, 헤더 추가
- **HTTP/1.1  1997년: 가장 많이 사용, 우리에게 가장 중요한 버전**

⇒ RFC2068 (1997) -> RFC2616 (1999) 개정 -> RFC7230~7235 (2014) 개정

- HTTP/2 2015년: 성능 개선
- HTTP/3 진행중: TCP 대신에 UDP 사용, 성능 개선

**◼️ HTTP 기반 프로토콜**

1) TCP 위에서 동작 : HTTP/1.1,  HTTP

2) UDP 위에서 동작 : HTTP/3

- 현재는 HTTP/1.1을 주로 사용
- HTTP/2, HTTP/3 도 점점 증가

**[부연 설명]**

- HTTP/1.1 ,  HTTP/2 같은 경우에는 TCP 프로토콜 위에서 동작한다.
- HTTP/3은 UDP 프로토콜 기반으로 개발이 되어있다.
- TCP는 3 way handshake도 해야 하고 기본적으로 데이터도 많고 매커니즘 자체가 속도가 느린 편이다.
- 그래서 UDP 프로토콜 위에 애플리케이션 단계에서 성능을 최적화하도록 새로 설계해서 나온 게 HTTP/3 이다.
- 아래의 그림에서 **‘프로토콜’ 하위에 h2로 적힌 건 http/2 버전이고, h3로 적힌 건 http/3 버전이다.**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/7136d84d-ac10-4bc2-ba0c-5a97fe0a3b0d/Untitled.png)

**◼️ HTTP 특징** 

- HTTP 프로토콜은 기본적으로 클라이언트-서버 구조이다.
- **무상태 프로토콜(stateless). 비연결성**
- HTTP 메시지를 통해 통신을 하다.
- **단순함, 확장 가능성**이 주요 특징이다.

### **⬛ 2. 클라이언트- 서버 구조**

**◼️ 클라이언트와 서버 구조**

- Request Response 구조
- 클라이언트는 서버에 요청을 보내고, 응답을 대기
- 서버가 요청에 대한 결과를 만들어서 응답

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/2cfc5eec-52d0-4691-b98d-3ee57a141105/Untitled.png)

- (표면적) HTTP는 클라이언트-서버 구조로 단순하게 되어있다.
- HTTP는 클라이언트가 HTTP 메시지를 통해서 서버에 요청을 보내고, 클라이언트는 서버에 응답이 올 때 기다린다.
- 서버가 요청에 대한 결과를 만들어서 응답이 오면 그 응답 결과를 열어서 클라이언트가 동작한다.

**◼️ 역할**

원래는 클라이언트와 서버가 하나로 되어있었다.

개념적으로 분리가 되면서 각자 독립적으로 진화되었다.

- 클라이언트 : UI, 사용성에 집중
- 서버: 비즈니스 로직, 데이터에 집중

이슈가 발생해도 서로의 역할이 달라 이슈에 대한 영향을 미치지 않고 양쪽이 독립적으로 이슈를 대응하며 진화가 가능해진 것이다.

### **⬛ 3. Stateful, Stateless 차이**

<aside>
💡 HTTP의 주요 특징 중 하나는 바로 ‘무상태 프로토콜’을 지향한다는 것이다.

무상태를 지향하기 때문에 서버 확장성이 높다.

</aside>

**◼️ 상태 유지 (stateful)**

1) 항상 같은 서버가 유지되어야 한다.

2) 그런데 중간에 서버가 장애나면 ? - 서버 교체 시 다시 처음부터 시작

- ‘상태 유지’는 서버가 클라이언트 상태를 보존한다.
- 클라이언트가 상품을 구입할 때 상품 정보와 결제 정보를 기존에 매칭되어있던 서버로 계속 유지해야 돼서 **서버를 늘릴 수가 없다.**
- **중간에 유지해야 할 서버에 장애가 발생한다면** 다른 서버로 바꾸어야 하는데, 클라이언트가 처음부터 다시 해당 서버에 정보를 요청해야 하는 수고스러움이 있다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/b2404354-09ce-46c3-9f1a-3b8896bbb5e6/Untitled.png)

**◼️ 무상태 (stateless) : 스테이트리스**

- 장점: 서버 확장성 높음 (스케일 아웃)
- 단점 : 클라이언트가 추가 데이터 전송

1) 아무 서버나 호출해도 된다.

2) 중간에 서버가 장애 나면 ? - 그냥 다른 서버로 교체해서 쭉 이용

- ‘무상태’ 는 서버가 클라이언트의 상태를 따로 보존하지 않는다.
- 클라이언트가 애초에 상품 구입 시 필요한 (상품 정보, 결제 정보)를 모두 담아서 요청을 하고, 서버에서는 상태 보존없이 응답만 한다.
- 중간에 서버가 장애 발생해도 클라이언트가 필요한 정보들을 이미 담고 있어서 다른 서버로 교체해도 그대로 응답받을 수 있다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/067da9ed-c99e-4707-99e4-32de8c57df60/Untitled.png)

**🟩 Statefull(상태유지), stateless(무상태) 차이 정리**

- 상태 유지 : 중간에 다른 서버 교체 시, 다시 상태 정보를 다른 서버에 알려줘야 한다.
- 무상태 : 중간에 다른 서버 무한 교체 가능하다.

      무상태는 응답 서버를 쉽게 바꿀 수 있다. → 무한한 서버 증설 가능 

**◼️ 무상태 스케일 아웃 - 수평 확장에 유리함**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/18f726bb-01b3-47bb-8f83-3848e7ae72a8/Untitled.png)

- 로그인 없이 검색만 할 경우 검색 서버에 트래픽이 몰려, 검색 서버에 클라이언트 상태를 유지하지 않아서 서버를 많이 늘릴 수 있다.
- 클라이언트-서버 아키텍쳐에서는 엄청난 확장성을 가져와 무한 서버 증식이 가능하다.

**◼️ 상태유지와 무상태의 한계**

**1) 상태 유지의 실무 한계**

- 로그인 해야 되는 경우 로그인한 사용자가 로그인 상태라는 상태를 서버에 유지해야 한다.
- 브라우저에서 쿠키와 서버의 세션을 같이 조합해서 상태를 유지하는 기능을 쓴다.
- 서버에서 세션 서버가 죽어버리면 전체적으로 로그인이 풀려버리게 된다.
- 로그인할 필요없는 단순 소개페이지의 경우 상태유지할 필요 없으니 굳이 사용할 필요가 없다.
- 따라서 **상태 유지는 ‘최소한’만 사용할 것.**

**2) 무상태의 실무 한계** 

- 모든 것을 무상태로 설계할 수 없는 경우도 있다. (ex. 로그인)
- **클라이언트가 전송할 때 필요한 정보를 모두 담아야 해서 데이터량이 많다.**

### **⬛ 4. 비연결성 (connectionless)**

**◼️ 연결을 유지하는 모델** 

- TCP/IP 연결 같은 경우 기본적으로 연결을 유지한다.
- 여러 클라이언트에서 서버로 응답을 요청하면 서버는 요청이 들어온 클러이언트마다 모두 연결을 유지해서 상태를 저장한다.
- 클라이언트가 많아질수록 연결을 유지하는 서버의 자원이 계속 소모되는 단점이 있다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/de77158d-376a-4bc1-905a-4e4f5e3e24ff/Untitled.png)

**◼️ 연결을 유지하지 않는 모델** 

- 클라이언트가 요청할 때마다 서버는 응답만 보내주고 즉시 연결을 종료하기 때문에, 서버가 최소한의 자원으로 유지할 수 있다.
- 요청할 때마다 연결하고 응답보낸 뒤에는 즉시 끊는다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/240a91b0-17d8-4446-8363-5795aa782429/Untitled.png)

**◼️ 비연결성** 

- HTTP는 기본적으로 ‘연결을 유지하지 않는’ 모델
- 일반적으로 초 단위 이하의 빠른 속도로 응답을 한다. ****
- 1시간 동안 수천명이 서비스 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이하로 매우 작아진다. 따라서 **서버 입장에서는 자원의 가용성이 훨씬 높다.**
- 서버 자원을 매우 효율적으로 사용할 수 있다.

**◼️ 비연결성의 한계와 극복**

- TCP/IP 연결을 새로 맺을 때마다 3 way handshake 시간 추가되어 클라이언트 입장에서는 느리다.
- 웹 브라우저로 사이트를 요청하면, HTML, CSS, Javascript, 추가 이미지 등 수많은 자원이 함께 다운로드할 때 연결하고 끊고, 또 연겨라고 또 끊고 하면 ‘비효율적’이다.
- 지금은 HTTP 지속 연결(Persistent Connections)로 문제 해결
- HTTP/2, HTTP/3에서 더 많은 최적화되어 있다.

**◼️ HTTP 초기 - 연결, 종료 낭비**

- 하나 받고 끊고, 연결하고 하나 받고 끊고, 연결함

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/5efb35da-62a7-45a8-8250-76c9c53caa26/Untitled.png)

**◼️ HTTP 지속 연결 - Persistent Connections**

- 모두 받을 때까지 응답을 유지하는 방식

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/c7fd4c96-0fb7-41a0-b25f-b74cb3f3594f/Untitled.png)

**◼️ Stateless를 기억하자.**

- 서버 개발자들이 어려워하는 업무가 같은 타이밍에 발생하는 대용량 트래픽이 발생할 때 처리하는 업무이다.
- 이럴 때는 Stateless하게 설계하는 것이 가장 중요하다.

### **⬛ 5. HTTP 메시지**

**◼️ HTTP 메시지 구조** 

- HTTP 메시지는 크게 4가지 구조로 나눌 수 있다.

1) start-line 시작 라인 

2) header 헤더

3) empty line(CRLF) 공백 라인 

4) message body

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/55b965d1-5f2e-4aa5-b238-f28fc16ba2b0/Untitled.png)

**◼️ HTTP 요청 메시지**  

```java
GET/search?q=hello&hl=ko HTTP/1.1
 메소드 / 요청 대상 / HTTP 버전
Host: www.google.com
```

**1) 시작 라인**

**(1) start-line = request-line**

**(2) request-line = HTTP메소드 SP(공백) 요청대상 SP HTTP-version CRLF(엔터)**

- HTTP 메소드 : GET/POST/PUT/DELETE 등이 있고 서버가 수행해야 할 동작을 지정
- 요청 대상 : 절대경로 “/”로 시작하는 경로. apsolute-path[?query] : 절대경로/?쿼리 형식
- HTTP 버전

**◼️ HTTP 응답 메시지** 

**(1) start-line = status-line**

**(2) status-line = HTTP-version SP(공백) 상태코드 SP(공백) 이유 문구 CRLF(엔터)**

- HTTP 버전
- HTTP 상태코드 : 요청 성공 or 실패 나타냄

200 : 성공 400 : 클라이언트 요청 오류 500 : 서버 내부 오류 

- 이유 문구 : 사람이 이해할 수 있는 짧은 상태 코드 설명 글

**◼️ HTTP 헤더 용도**

- HTTP 전송에 필요한 모든 부가 정보 담김
- 예 ) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보 …
- 표준 헤더가 너무 많음
- 필요시 임의의 헤더 추가 가능

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/83ea7154-b4c4-4568-b9eb-d81d6a070839/Untitled.png)

**◼️ HTTP 메시지 바디 용도**

- 실제 전송할 데이터
- HTML 문서, 이미지, 영상, JSON 등 byte로 표현할 수 있는 모든 데이터 전송 가능

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/205452df-d55a-464b-a089-6f34bce2fc1a/Untitled.png)

### 🟩 정리

- HTTP는 단순함과 확장 가능성이 큰 특징이다.
- HTTP 메시지에 모든 것을 전송
- HTTP 역사, HTTP/1.1 을 기준으로 학습
- 클라이언트-서버 구조
- 무상태 프로토콜(stateless)
- HTTP 메시지
- 단순함, 확장 가능
- 지금은 HTTP 시대