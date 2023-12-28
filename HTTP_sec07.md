## **🟦 섹션 7. HTTP 헤더 1 - 일반 헤더**

### **⬛ 1. HTTP 헤더 개요**

**◼️ HTTP 헤더** 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/495ef540-2c02-485c-aeab-18e2b186db24/Untitled.png)

**◼️ HTTP 헤더 용도**

- **HTTP 전송에 필요한 모든 부가 정보를 담음**
- HTTP 전송에 필요한 **[메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리]** 등 모든 부가 정보를 헤더에 넣는다.
- 표준 헤더가 굉장히 많다.
- 필요 시 임의의 헤더 추가도 가능하다.

**◼️ HTTP 헤더 분류 - RFC2616 (과거)**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/abda8dbf-9234-4307-b129-9d6a9202311c/Untitled.png)

**[헤더 분류]** 

- **General 헤더 :** 메시지 **‘전체’**에 적용되는 정보 예) Connection:close
- **Request 헤더 :** 요청 보낼 때 들어가는 정보  예) User-Agent: Mozilla/5.0 (Macintosh; ) :
- **Response 헤더 :** 응답 정보 예) Server, Apache
- **Entity 헤더 :** 엔티티 바디 정보 예) Content-Type: text/html,  Content-Length:3423

**◼️ HTTP Body - message body - RFC2616(과거)**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/6e778077-6226-4434-9b02-cf470bd0b271/Untitled.png)

- 메시지 본문은 엔티티 본문을 전달하는데 사용한다.
- 엔티티 본문 : 요청이나 응답에서 전달할 ‘실제 데이터’
- **엔티티 헤더**는 **엔티티 본문 데이터를 해석할 수 있는 정보를 제공**한다.

EX) 데이터 유형(html, json), 데이터 길이, 압축 정보 

**◼️ 그런데 스펙이 바뀐다!** 

- 1999년 ~~RFC2616~~ - 폐기 (위에 나온 내용)
- **2014년 RFC7230~7235 등 (개정)**

**◼️ RFC723X 변화**

- 엔티티(Entity) →  표현(Representation)
- Representation = representation Metadata + Representation Data
- 표현 = 표현 메타데이터 + 표현 데이터

### **⬛ 2. 표현**

**◼️ HTTP 표준 - RFC723X 변화**

- 엔티티 → 표현으로 바뀌게 되었다.
- 표현 : 메타 데이터 + 표현 데이터 ****

**◼️ HTTP Body - message body - RFC7230(최신)**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/7bb9e398-da1c-4223-b208-099a385b068d/Untitled.png)

- **메시지 본문을 통해 표현 데이터를 전달**
- 메시지 본문 = 페이로드(payload)
- 표현 = 요청이나 응답에서 전달할 실제 데이터
- 표현 헤더 = 표현 데이터를 해석할 수 있는 정보 제공

ex. 데이터 유형(json, html), 데이터 길이, 압축 정보 등

- 참고: 표현 헤더는 표현 메타 데이터와, 페이로드 메시지를 구분해야 하지만, (여기선 생략)

**◼️ 표현 (Represantation)**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/0d2740e7-d7ea-40e7-aa42-939061ef7b4f/Untitled.png)

- **Content-Type :**  표현 데이터의 형식
- **Content-Encoding:** 표현 데이터의 압축 방식
- **Content-Language :** 표현 데이터의 자연 언어
- **Content-Length :** 표현 데이터의 길이

표현 헤더는 전송, 응답 둘다 사용 O

**◼️ Content-Type | 표현 데이터의 형식 설명**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/ea8e0298-0915-4780-a427-372f4fc2592a/Untitled.png)

- 표현 데이터 **형식 설명**하기 위해 사함
- 미디어 타입, 문자 인코딩

예) text/html; charset=utf-8

예) application/json

예) image/png

<aside>
💡 회원 리소스를 HTML 형식으로 전송할지 JSON으로 전송할지 실제리소스는 추상적이다. DB에 있을수도 있고, Bytecode로 어딘가 저장되어 있을수 있고 파일로 되어있을 수 있다. 클**라이언트랑 서버 간에 실제 주고 받을 떄 이해할 수 있는 뭔가를 변환해서 데이터 전달해야 한다. 이때 ‘헤더’에다가 Content-Type을 사용하여 전달할 데이터의 형식을 설명해준다.**

</aside>

 

**◼️ Content-Encoding | 표현 데이터 인코딩**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/3440129a-7594-4ec9-981f-964e7cae3597/Untitled.png)

- 표현 데이터를 **압축**하기 위해 사용함
- **데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가**
- **데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제**

예) gzip, deflate, identity

<aside>
💡 표현 데이터를 압축하기 위해 사용한다. 서버에서 클라이언트에 보낼 떄 Content-Encoding 부가 정보를 보내줘야 무엇으로 압축되는지 알 수 있다. 데이터 전달하는 곳에서 압축 후 인코딩 추가하고 데이터를 읽는 쪽에서 인코딩 헤더 정보로 압축을 해제한다.

</aside>

**◼️ Content-Language | 표현 데이터의 자연 언어**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/b6c78755-82de-4bb2-8525-51d90384c739/Untitled.png)

- 표현 데이터의 **자연 언어**를 표현함

예) ko,  en,  en-US 등

**◼️ Content-Length | 표현 데이터의 길이**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/9bcfa644-16a5-4c70-8a41-b9027ffcc617/Untitled.png)

- 표현 데이터의 **길이**를 표현한다.
- 바이트 단위
- Transfer-Encoding(전송 코딩)을 사용하면 그 안에 정보가 다 담겨있기 때문에 Content-Length를 사용하면 안됨

### **⬛ 3. 콘텐츠 협상**

**◼️ 협상 | 클라이언트가 선호하는 표현 요청** 

**협상 : 클라이언트가 원하는 표현을 달라고 서버한테 요청을 하면 서버가 클라이언트가 원하는 우선순위에 맞춰서 표현 데이터를 만들어 보낸다.**

- **Accept :** 클라이언트가 선호하는 **미디어 타입** 전달
- **Accept-Charset :** 클라이언트가 선호하는 **문자 인코딩**
- **Accept-Encoding :** 클라이언트가 선호하는 **압축 인코딩**
- A**ccept-Language :** 클라이언트가 선호하는 **자연 언어**

협상 헤더는 **요청** 시에만 사용

한국어 브라우저를 사용하고 다중 언어 지원하는 서버를 사용한다고 가정 하에 한국어 브라우저는 외국 사이트를 /event로 들어갔다고 치자. 이떄 서버는 내부적으로 우선순위가 기본 영어를 보내지만 한국어도 지원한다. 

**◼️ Accpet-Langugae 적용 전 | Before**

- 클라이언트에서 서버로 보낼 때 **클라이언트가 한국어를 원하는지 영어를 원하는지 아무 정보가 없다.**
- 그래서 **서버는 기본값인 영어 관련 내용으로 한국어 브라우저에 응답**해준다,

**◼️ Accpet-Langugae 적용 후 | After**

- **클라이언트가 선호하는 언어가 ‘한국어’임을 입력**해서 서버에게 전달했다.
- **서버는** 기본 언어가 영어이지만 한국어도 지원하고 있기 떄문에, **클라이언트가 원하는 한국어로 데이터를 전달한다.**

**◼️ Accept-Language 복잡한 예시  → 우선순위의 필요성**

- **클라이언트가 선호하는 언어는 한국어라고 서버에게 전달**한다.
- 이떄 **해당 서버의 기본 언어는 독일어인데 영어를 지원**한다고 하자.
- (클라이언트는 한국어를 원하지만, 독일어는 모르니 영어를 원한다.)
- 다중 언어 지원 **서버가 한국어를 지원하지 않으니 그냥 기본 언어인 독일어로 보내게 된다.**

→ 이러한 복잡한 상황이 있을 수 있으므로 ‘우선 순위’가 필요하게 된다.

**◼️ 협상과 우선순위 1 | Quality Values(q)**

- **Quality Values(q) 값 사용**
- **0 - 1, 클수록 높은 우선순위 가짐**
- 생략하면 1

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/0b7ede08-f01e-44ef-9940-ae9a94eb3096/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/9870888e-2fb3-44c4-9b48-2d590cd14067/Untitled.png)

- **위 그림에서 우선순위가 Accept-Language 에 담겨 서버로 보내졌다.**
- **서버는 기본 독일어를 지원하고 영어도 지원하는데, 이때 우선순위도 함께 존재하므로 우선순위에 따라 클라이언트가 독일어보다는 더 선호하는 영어로 응답한다.**

**◼️ 협상과 우선순위 2 | 구체적인 것이 우선한다.**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/d70ae085-c7a5-4c89-a8dc-183dc54aa497/Untitled.png)

**◼️ 협상과 우선순위 3 | 구체적인 것을 기준으로 ‘미디어 타입’을 매칭된다.**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/2afb5fd9-442d-4c60-ad81-35dca2d0b0fe/Untitled.png)

### **⬛ 4. 전송 방식**

**◼️ 전송 방식 4가지 관련 헤더들**

1) 단순 전송

2) 압축 전송

3) 분할 전송

4) 범위 전송

**◼️ 단순 전송 | Content-Length**

- **Content 길이를 지정**해서 **한 번에 요청하고 응답**한다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/2d097650-56c6-40bb-a644-bf58e4e2e0d6/Untitled.png)

**◼️ 압축 전송 | Content-Encoding**

- Content를 압축할 때 **무엇으로 압축되어 있는지 정보를 함께 전송한다.**
- 그래야 클라이언트에서 알고 압축을 풀 수 있기 때문에 압축 정보를 주는 것이다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/029dc31b-6c18-45a8-911a-e64634be4d1f/Untitled.png)

**◼️ 분할 전송 | Transfer-Encoding**

- chunked : 덩어리 라는 뜻
- 분할 전송은 덩어리로 쪼개서 전송한다.
- **분할 전송할 때는 Content-Length를 넣으면 안된다!!**

[그림 설명]

- 5byte로 hello를 서버에서 클라이언트로 보낸다.
- 또 5byte로 world를 보내고
- 마지막으로 0byte로 src를 보내면 끝이라는 것을 표현한다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/bfb8ac25-9435-477e-9749-06b56287186a/Untitled.png)

**◼️ 범위 전송 | Content-Range**

- 이미지를 받았는데 **중간에 끊길 경우 못 받은 범위를 지정해서 다시 요청한다.**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/90c261a7-12f0-4849-b301-250b035913b6/Untitled.png)

### **⬛ 5. 일반 정보**

- HTTP 정보성 헤더들

**◼️ 일반 정보** 

- From : 유저 에이전트의 이메일 정보
- Referer: 이전 웹 페이지 주소
- User-Agent : 유저 에이전트 애플리케이션 정보
- Server : 요청을 처리하는 오리진 서버의 소프트웨어 정보
- Date : 메시지가 생성된 날짜

**◼️ From | 유저 에이전트의 이메일 정보**

- 일반적으로 잘 사용 되지 X
- 검색 엔진 같은 곳에서 주로 사용
- 요청에서 사용

**◼️ Referer | 이전 웹 페이지 주소**

- 현재 요청된 페이지의 이전 웹 페이지 주소
- A→B로 이동하는 경우, B를 요청할 때 [Referer: A]를 포함해서 요청
- Referer을 사용하여 유입 경로 분석 가능
- 요청에서 사용

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/2d008631-dc15-4f7f-83f6-9ca4ee128e24/Untitled.png)

**◼️ User-Agent | 유저 에이전트 애플리케이션 정보**

- **클라이언트의 애플리케이션 정보** (웹 브라우저 정보, 등)
- 통계 정보
- **사용자들이 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능**
- 요청에서 사용

**◼️ Server | 요청을 처리하는 Origin 서버의 소프트웨어 정보**

- Server : Apache/2.2.22(Debian)
- server : nginx
- 응답에서 사용

**◼️ Date | 메시지가 발생한 날짜와 시간**

- 메시지가 발생한 날짜와 시간이다.
- 응답에서만 사용한다.

### **⬛ 6. 특별한 정보**

- 특별한 정보를 제공하는 HTTP 헤더

**◼️ 특별한 정보**

- Host : 요청한 호스트 정보(도메인)
- Location: 페이지 리다이렉션
- Allow: 허용 가능한 HTTP 메서드
- Retry-After: 유저 에이전트가 다음 요청 하기까지 기다려야 하는 시간

**◼️ Host | 요청한 호스트 정보(도메인)**

- 요청에서 사용하고 필숫값이다.
- **하나의 서버가 여러 도메인을 처리해야 할 때 or 하나의 IP 주소에 여러 도메인이 적용되어 있을 때 ‘구분해줘야 한다.’**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/08353618-c857-4afb-9a82-9d6a5e44b3f8/Untitled.png)

**◼️ Location | 페이지 리다이렉션**

- 웹 브라우저는 3xx 응답 결과에 Location 헤더가 있으면, Location 위치로 자동 이동(리다이렉트)
- 응답코드 3xx에서 설명
- 201 (Created) : Location 값은 요청에 의해 생성된 리소스 URI
- 3xx (Redirection) : Location 값은 요청을 자동으로 리다이렉션 하기 위한 대상 리소스를 가리킴

**◼️ Allow | 허용 가능한 HTTP 메서드**

- 405 (Method Not Allowed)에서 응답에 포함해야 함
- Allow : GET, HEAD, PUT만 지원한다.
- | 단, 서버에서는 많이 구현되지 않는다.

**◼️ Retry-After | 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간**

- 503(Service Unavailable) : 서비스가 언제까지 불능인지 알려준다.
- Retry-After : 날짜 표기, 초단위 표기

### **⬛ 7. 인증**

- 인증 정보를 헤더로 보낸다.

**◼️ 인증** 

- Authorization : 클라이언트 인증 정보를 서버에 전달
- WWW-Authenticate : 리소스 접근 시 필요한 인증 방법 정의한다.

### **⬛ 8. 쿠키**

- Set-Cookie : **서버에서** 클라이언트로 **쿠키 전달 (응답)**
- Cookie : **클라이언트가** 서버에서 받은 쿠키를 **저장하고**, **HTTP 요청 시 서버로 전달**

**◼️ 1) 쿠키 미사용 상황**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/c76f95be-eecf-4982-a97d-3b3cf1da46c3/Untitled.png)

(1) **비회원 접근** |  웹 브라우저에 로그인 안한 사용자가 /welcome 으로 웹 페이지에 접근하면 서버 입장에서는 회원이 아닌 손님으로 들어오는 것이다.

(2) **비회원이 로그인 시도** | /login 으로 유저 정보, 패스워드 등을 POST 방식으로 보내서 로그인 시도하면 서버에서는 해당 user가 로그인 했다고 응답해준다. 

(3) **다시 접근** | 이 상태에서 다시 /welcome으로 접근 시, 서버 입장에서는 로그인한 사용자인지 아닌지 구분할 수 있는 방법을 모른다. 

**→ 이러한 이유는 HTTP가 무상태 프로토콜이기 때문이다.**

(4) **쿠키 미사용 시 대안** : 모든 요청에 사용자 정보를 포함

- 모든 요청에 항상 사용자 정보를 포함해서 보내면 ‘회원’ user인지 구분은 할 수 있다.
- 사용자 정보를 계속 서버에 주면 서버는 해당 user가 회원인지 응답해준다.

**문제 1 : 모든 요청에 사용자 정보가 포함되도록 개발해야 함 → 수고스러**

**문제 2 : 보안 문제** 

### >> Stateless 무상태 프로토콜

- HTTP는 무상태(Stateless) 프로토콜이다.
- 클라이언트와 서버가 요청과 응답을 주고 받으면 연결이 끊어진다.
- 클라이언트가 다시 요청하면 서버는 이전 요청을 기억하지 못한다.
- 클라이언트와 서버는 서로 태를 유지하지 않는다.

**◼️ 2) 쿠키 사용 상황**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/4ce46219-a2e0-4465-9c46-26eefb6d8d3c/Untitled.png)

(1) **비회원 접근** |  웹 브라우저에 로그인 안한 사용자가 /welcome 으로 웹 페이지에 접근하면 서버 입장에서는 회원이 아닌 손님으로 들어오는 것이다.

(2) **비회원이 로그인 시도 |** 웹 브라우저가 POST로 로그인을 하면 서버에서는 Set-Cookie 로 회원 정보를 만들어서 응답한다.

(3) **쿠키 저장소에 저장됨** | 웹 브라우저 내부에서는 ‘쿠키 저장소’가 있는데, 서버가 응답에서 만든 Set-Cookie를 쿠키 저장소에 key = user, value = 정보 로 저장한다.

(4) **다시 접근 |** 로그인 이후 해당 회원이 다시 /welcome 페이지로 접근 하면 자동으로 웹 브라우저는 서버에 요청 보낼 때마다 쿠키 저장소에서 조회 후 해당 회원의 정보를 HTTP 헤더에 담아서 서버에 함께 보낸다.

(5) **다시 접근 |** 서버는 요청이 들어온 상태에서 쿠키 열어보니 회원인 걸 인지하기 때문에, 따로 URL이나 파라미터로 정보를 담을 필요가 없어진다.

지정한 서버에 쿠키는 모든 요청 정보에 쿠키 정보를 자동으로 포함한다.  

**◼️ 쿠키** 

```java
ex) set-cookie : sessionId = abcde1234; expires=Sat, 26-Dec-2023 00:00:00 GMT; path=/; domain=.google.com;Secure
```

**사용처**

- 사용자 로그인 세션 관리
- 광고 정보 트래킹

**쿠키 정보는 항상 서버에 전송됨**

- 네트워크 트래픽 추가 유발
- 최소한의 정보만 사용 (세션id, 인증 토큰)
- 서버에 전송하지 않고, 웹 브라우저 내부에 데이터 저장하고 싶으면 웹 스토리지 (localStorage, sessionStorage) 참고

**주의 !**

- 보안에 민감한 데이터는 저장하면 안됨(주민번호, 신용카드 번호 등)

**◼️ 쿠키 - 생명주기 | expires, max-age**

🎈 **expires** 

쿠키를 무제한 보관할 수 없다. GMT 기준으로 만료일이 되면 쿠키를 자동 삭제한다.

- Set-Cookie : expires=Sat, 26-Dec-2020 04:39:21 GMT

🎈 **max-age**

초 단위로 구성되어 있고 0이나 음수를 지정하면 쿠키가 삭제된다.

- Set-Cookie: max-age = 3600 (3600초)

**◼️ 쿠키 - 종류**

🎈 **세션 쿠키 :** 만료 날짜를 생략하면 브라우저 종료시까지만 유지 

🎈 **영속 쿠키 :** 만료 날짜를 입력하면 해당 날짜까지 유지 

**◼️ 쿠키 - 도메인**

🎈 **명시 :** 도메인을 명시하면 명시한 문서 기준 도메인과 서브 도메인을 포함해서 다 전송한다.

-example.org 지정을 해서 쿠키를 생성하면 [dev.example.org](http://dev.example.org) 도 쿠가 같이 접근할 수 있다.

🎈 **생략 :** [example.org](http://example.org) 에서 쿠키를 생성했는데 도메인을 지정하는 걸 생략한다.

-example.org에서는 쿠키를 접근할 수 있어도 하위 도메인인 dev.example.org는 쿠키를 접근할 수 없다.

**◼️ 쿠키 - 경로**

**경로를 포함한 하위 경로 페이지만 쿠키를 접근할 수 있다.** 

일반적으로 path=/루트 경로로 지정한다.

예 ) path = /home  을 지정했다면

- /home (가능)
- /home/level1 (가능)
- /home/level1/level2 (가능)
- /hello (불가능)

**◼️ 쿠키 - 보안** 

**🎈 Secure**

- 쿠키는 http, https를 구분하지 않고 전송
- Secure를 적용하면 https인 경우에만 전송한다.

**🎈 HttpOnly**

- XSS 공격 방지
- 자바스크립트에서만 접근 불가 (document.cookie)
- HTTP 전송에만 사용

**🎈 SameSite**

- XSRF 공격 방지
- 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송