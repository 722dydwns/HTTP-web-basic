## **🟦 섹션 2. URI와 웹 브라우저 요청 흐름**

### **⬛ 1. URI | Uniform Resource Identifier**

- 뜻 : 리소스를 식별하는 통합된 방삭
- URI는 로케이터 (Locator), 이름(Name) 또는 둘 다 추가로 분류될 수 있다.
- 즉, URI 내부에 URL, URN이 포함된 구조이다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/1baac22a-702a-449c-9bdc-26d8b66b869f/Untitled.png)

**(1) Uniform Resource Locator | URL - 리소스가 있는 위치 지정 → 多 사용**

ex. [https://www.google.com:8080/over/there?nam](https://www.google.com:8080/over/there?name)e=ferret#nose

**(2) Uniorm Resource Name | URN - 리소스에 이름 부여 → 매핑 어려움**

ex. urn:example:animal:ferret:nose 

**◼️ URI 단어 뜻** 

1) U : Uniform : 리소스 식별하는 통일된 방식

2) R : Resource : 자원, URI로 식별할 수 있는 모든 것 (제한 X)

3) I : Identifier : 다른 항목과 구분하는데 필요한 정보

**◼️ URL, URN 단어 뜻**

1) URL - Locator : 리소스가 있는 위치를 지정

2) URN - Name : 리소스에 이름을부여 

→ URN 이름 만으로 실제 리소스 찾는 방식이 보편화되지 않았음

**→ 따라서 앞으로는 URI == URL과 같은 의미로 이야기 하겠다.**

### **◼️ URI 전체 문법 분석**

```java
[예시] https://www.google.com/search?q=hello &hl=ko

[구조] 스키마:// [userInfo] host [:port] [/path] [?query] [# fragment]
```

- **스키마 : 프로토콜(https)**
- **호스트명 (www.google.com)**
- **포트번호 (443)**
- **패스 (/search)**
- **쿼리 파라미터 (q=hello & hl = ko)**

**◼️ URL schema | 스키마**

- 주로 프로토콜 사용
- 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙

ex) http, https, ftp 등

- http는 80포트, https는 443 포트를 주로 사용, 포트는 생략 가능
- https는 hssp secure로서 강력한 보안 추가된

**◼️ URL host | 호스트명**

- 호스트명
- 도메인명 or IP 주소를 직접 사용 가능

**◼️ URL PORT | 포트**

- 포트
- 접속 포트
- 일반적으로 생략, 생략 시 http는 80, https 는 443

**◼️ URL path | 경로**

- 리소스 경로(path), 계층적 구조

 /home/file.jpg

/members/100

/items/iphone12

**◼️ URL query | 쿼리**

- key = value 형태
- ?로 시작, &으로 추가 가능

?keyA=valueA&&keyB=valueB

- 쿼리 파라미터, 쿼리 스트링으로 불린다.
- 웹 서버에 제공하는 파라미터이며 문자 형태

**◼️ URL fragment | 프래그먼트**

- 잘 사용하진 않는다.
- html 내부 북마크 등에 사용
- 서버에 전송되는 정보는 아

### **⬛ 2. 웹 브라우저 요청 흐름**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/6ffc312c-7f55-40f8-a64f-6ab175c50c27/Untitled.png)

1) URL을 입력한다.

2) DNS 서버로 해당 IP를 찾아내고, 생략된 PORT는 schema로 찾아낸다.

3) 웹 브라우저가 HTTP 요청 메시지 생성한다.

4) SOCKET 라이브러리를 통해 TCP/IP로 IP와 PORT 정보 찾은 거를 3 way handshake 방식으로 서버와 연결한다.

5) HTTP 요청 메시지는 OS 에 있는 TCP/IP 계층으로 전달된다.

6) TCP/IP 계층에서 HTTP 요청 메시지에 패킷으로 감싼다.

7) 웹 브라우저가 만든 요청 패킷을 서버에서 도착하면 패킷을 열어 HTTP 요청 메시지를 확인해서 서버가 해석한다.

8) 서버가 HTTP 응답 메시지를 만들어서 TCP/IP 패킷을 감싸서 클라이언트에게 돛가하면 패킷을 열어서 HTTP 응답 메시지를 확인해서 클라이언트가 해석한다.

9) 웹 브라우저가 HTML 렌더링을 해서 클라이언트가 HTML 결과를 볼 수 있다.