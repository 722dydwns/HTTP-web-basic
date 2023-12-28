## **🟦 섹션 5. HTTP 메서드 활용**

### **⬛ 1. 클라이언트에서 서버로 데이터 전송**

**◼️ 데이터 전달 [방식] | 크게 2가지** 

**1) ‘쿼리 파라미터’를 통한 데이터 전송** 

- GET
- 주로 정렬 필터(검색어)

**2) ‘HTTP 메시지 바디’를 통한 데이터 전송**

- POST, PUT, PATCH
- 회원가입, 상품 주문, 리소스 등록, 리소스 변경

**◼️ 데이터 전달 [상황] | 크게 4가지** 

**1) 정적 데이터 조회**

- 이미지, 정적 text 문서

**2) 동적 데이터 조회**

- 주로 검색, 게시판 목록 정렬 필터(검색어)

**3) HTML FORM을 통한 데이터 전송**

- 회원가입, 상품주문,데이터 변경

**4) HTTP API를 통한 데이터 전송** 

- 회원가입, 상품주문, 데이터 변경
- 서버 to 서버, 앱-클라이언트, 웹-클라이언트(Ajax)

**◼️ 1) 정적 데이터 조회 | 쿼리 파라미터 미사용** 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/d7a03d3e-32e0-4440-9cd6-c65f14522756/Untitled.png)

- 클라이언트에서 static/star.jpg 로 요청 메시지를 보내면
- 서버에서 받은 리소스 경로의 star.jpg 이미지를 그대로 클라이언트에 응답해준다.

‘**정적 데이터’는 일반적으로 쿼리 파라미터 없이 단순 리소스 경로로 조회가 가능하다.**

정적 데이터 조회 시 이미지나 정적 텍스트 문서로 조회하기 때문에 GET으로 사용한다.

**◼️ 2) 동적 데이터 조회 | 쿼리 파라미터 사용** 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/4b8a6ef1-2b27-4223-b051-b450a955d06d/Untitled.png)

구글에서 검색할 때 ‘검색어’나 추가  조건에 대한 데이터를 전달할 때 사용 多

- 클라이언트는 쿼리 파라미터들을 사용해서 서버에게 요청한다.
- 서버는 쿼리 파라미터를 기반으로 key-value로 꺼내서, 정렬 필터 후 결과를 동적으로 생성한뒤 클라이언트에게 응답한다.

주로 검색, 게시판 목록 정렬, 필터 시, 추가 데이터들을 함께 쿼리 파라미터로 요청한다.

조회 조건을 줄여주는 필터, 조회 결과를 정렬하는 정렬 조건에 주로 사용한다.

이것도 여전히 ‘조회’여서 GET 방식으로 사용한다.

**◼️ 3) HTML Form 데이터 전송** 

**[POST 전송 - 저장]**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/a4334f31-fe74-45c6-8b95-03f2e1dcfaa1/Untitled.png)

그림에서 form 태그에서 action은 /save, 메소드는 POST이다.

**1) input 폼에 클라이언트가 username과 age 정보를 입력 후 ‘전송’ 버튼 누르면**

**2) ’웹 브라우저’가 폼 데이터를 읽어서 HTTP 메시지를 생성한다. 쿼리 파라미터와 유사하게 key-value 형식으로 데이터를 만들어서 HTTP 바디에 넣고 POST 방식으로 서버에 전송한다.** 

**3) 그러면 서버에서 해당 데이터를 저장한다.** 

~~**[GET 전송 - 저장]**~~

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/68dbdd0d-1e44-4abf-8104-4eaed9c791b1/Untitled.png)

그런데, 똑같이 save (저장)을 위해 form을 통해서 데이터 전송을 시도할 때 **GET메소드로 변경하면 ‘웹 브라우저’는 GET이 메시지 바디를 보통 사용하지 않기 때문에 그냥 쿼리 파라미터에 넣고 서버에 전달한다.**

- save나 리소스를 변경할 때 GET 메소드를 사용하면 안된다.
- GET은 오직 조회할 때 사용한다.

**[GET 전송 - 조회]**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/b1471f64-668f-48f0-ad90-974631deb8b6/Untitled.png)

이제 form을 통해서 GET 방식으로 ‘조회’를 한다.

**웹 브라우저가 생성한 HTTP 메시지에 쿼리 파라미터 형식으로 username = 김, age = 20 로 담아서 서버에 전달한다.**

- 그러면 서버는 받은 데이터 정보를 기준으로 필터링해서 조회한 결과를 클라이언트에게 응답할 것이다.

[**멀티 파트 폼 데이터]** **[multipart/form-data] : 폼으로 파일 전송할 때 사용**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/a60ce030-7604-4c63-b977-79c98127582c/Untitled.png)

메시지 바디에 username과 age뿐 아니라 바이트로 되어있는 ‘파일’까지 POST 메소드로 전송하고 있다.

이때  웹 브라우저가 생성한 요청 HTTP 메시지의 Content-type은 multipart/form-data 데이터로 들어가고,  boundary는 자동 생성되어 경계로 나눠진다.

### **🟩 HTML Form을 통한 데이터 전송 정리**

**1) HTML Form을 통해 POST 방식 전송한다.**

보통 회원 가입하거나 상품 주문하거나 데이터를 변경할 때 주로 사용한다.

**2) [기본] Content-type은 application/x-www-form-urlencoded방식이다.**

이때 form의 내용을 HTTP 바디에 key-value 형식의 쿼리 파라미터를 보낸다. 전송 데이터를 url encoding 처리한다.

**3) HTML Form은 GET 전송도 가능하다.**

**4) Content-Type으로 multipart/form-data 은 파일 업로드 같은 바이너리 데이터를 같이 전송할 수 있다.**

이때 다른 종류의 여러 파일과 폼의 내용  함께 전송 가능하다.

**5) 참고: HTML Form 전송은 GET/POST만 지원한다.**

**◼️ 4) HTTP API 데이터 전송** 

- 클라이언트에서 HTTP API로 서버에 데이터를 전송하는데, 직접 만들어서 전송하면 된다.
- 클라이언트에 /members, Content-type은 application/json으로 데이터 전송한다.

### **🟩 HTTP API를 통한 데이터 전송 정리**

1) 서버 to 서버

- 백엔드 시스템 통신

**2) 앱 클라이언트**

- 아이폰, 안드로이드

**3) 웹 클라이언트**

- HTML에서 form 전송 대신 자바 스크립트 통한 통신에 사용 (AJAX)
- 예 ) React, Vue.js 와 같은 웹 클라이언트와 API 통신

**4) POST, PUT, PATCH : 메시지 바디를 통해 데이터 전송** 

**5) GET: 조회, 쿼리 파라미터로 데이터 전달**

**6) Content-Type : application/json을 주로 사용 (사실상 표준)**

- TEXT, XML, JSON 등

---

### **⬛ 2. HTTP API 설계 예시**

**◼️ POST 기반 데이터 등록**

→ 클라이언트가 서버에 회원을 등록해달라고 ‘요청’을 해서 서버가 리소스의 URI를 결정하고 만들어서 보내는 형태이다.

[ **회원 관리 시스템 API 설계 ]**

*여기서 리소스는 ‘회원’이다.

- **회원** 목록 /members ⇒ **GET**
- **회원** 등록 /members ⇒ **POST**
- **회원** 조회 /members/{id} ⇒ **GET**
- **회원** 수정 /members/{id} ⇒ **PATCH, PUT, POST**
- **회원** 삭제 /members/{id} ⇒ **DELETE**

**클라이언트는 등록될 리소스의 URI를 모른다.**

→ 회원 등록 /members ⇒ POST

→ POST/members 

**서버가 새로 등록된 리소스 URI를 결정하고 생성해준다.**

→ HTTP/1.1 201 Created

→ Location: **/members/100 (새로 생성된 URI)**

⇒ ‘**컬렉션’은 서버가 관리하는 리소스 저장소이다.**

**컬렉션 (Collection)**

→ 서버가 관리하는 리소스 디렉토리

→ 서버가 리소스의 URI를 생성하고 관리

→ 여기서 컬렉션은 **/members**

즉. 클라이언트는 등록할 리소스의 URI를 모르는 상태에서, 회원 데이터를 서버에 요청하게 되면 서버가 알아서 회원을 식별해서 URI를 만들어주는 형태인 것이다. 

**◼️ PUT 기반 데이터 등록**

→ PUT 기반 등록 시에는 클라이언트가 이미 등록될 리소스의 URI를 알고 있는 상태에서 지정하여 등록 요청을 한다

→ 서버는 그냥 지정해서 들어온 해당 URI로 등록 처리 후 반환한다.

**[ 파일 관리 시스템 API 설계 ]**

- **파일** 목록 /files **⇒ GET**
- **파일** 조회 /files / {fileName} **⇒ GET**
- **파일** 등록 /files / {fileName} **⇒ PUT**
- **파일** 삭제 /files / {fileName} **⇒DELETE**
- **파일** 대량 등록  /files **⇒ POST**

**PUT의 경우, 클라이언트가 리소스의 URI를 알고 있어야 한다.**

→ 파일 등록 /files/{fileName} ⇒ PUT

→ PUT /files/star.png

**클라이언트가 직접 리소스의 URI를 지정해서 생성된 리소스를 관리해야 한다.**

⇒ ‘**스토어’는 클라이언트가 관리하는 리소스 저장소이다.**

**스토어 (Store)**

- 클라이언트가 관리하는 리소스 저장소
- 클라이언트가 리소스의 URI를 알고 관리한다.
- 여기서 스토어는 **/files**

<aside>
💡 대부분 POST 기반의 컬렉션 사용하는 경우가 多

</aside>

**◼️ HTML Form 사용하여 데이터 등록**

- HTML Form은 **GET, POST만 지원**된다. → 제약이 있다.
- **컨트롤 URI**

**GET, POST만 지원하므로 제약이 있다.**

이런 제약 해결 위해 **‘동사’로 된 리소스 경로를 사용하는데 이게 컨트롤 URI 이다.**

**POST의 /new, /edit, /delete가 컨트롤 URI**

**HTTP 메서드로 해결하기 애매한 경우 사용한다.**

<aside>
💡 보통 리소스는 ‘명사’로 되어 있어야 한다. 경로에는 /members/GET 이런 식으로 해당 리소스로 해야 할 활동을 GET,POST,PUT,DELETE로 명시해주는 경우가 많다. 그러나 HTML Form에서는 GET과 POST만 지원하기 때문에 불가피하게 ‘동사’로 리소스 경로를 활용해야 하는 상황이 온다. 최대한 적게 사용해야 하지만, **이렇게 불가피할 경우 ‘컨트롤 URI’를 활용하는 것이다.**

</aside>

**[ 회원 관리 시스템 ]**

- **회원** 목록 /members **⇒ GET**
- **회원 등록 폼**  /members/new **⇒ GET**
- **회원 등록**  /members/new, /members **⇒ POST**
- **회원 조회** /members/{id} **⇒ GET**
- **회원 수정 폼** /members /{id}/ edit **⇒ GET**
- **회원 수정**  /members//{id}/ edit,  /members/{id} **⇒ POST**
- **회원 삭제** /members /delete **⇒ POST**

**🟩 섹션 5 정리**

**HTTP API - ‘컬렉션’**

- **POST 기반 등록**
- 서버가 리소스 URI를 결정한다.

**HTTP API - ‘스토어’**

- **PUT 기반 등록**
- 클라이언트가 리소스 URI를 결정한다.

**HTTP FORM 사용** 

- 순수 HTML + HTML Form 사
- **GET과 POST 만 지원**

### 🟩 **API를 설계 시 아래와 같이 4가지 설계 개념 참고하자.**