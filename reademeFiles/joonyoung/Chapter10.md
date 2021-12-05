# 5. REST API란

## 1) API
`API(Application Programming Interface 애플리케이션 프로그래밍 인터페이스, 응용 프로그램 프로그래밍 인터페이스)는 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 의미합니다.`  
<br/>
**역시나 쉽게 이해되지 않습니다.**

`고객 <- 키오스크 -> 요리사`

`프로그램 <- API -> 프로그램`

위 처럼 생각하면 이해하는데 조금은 도움을 줍니다.

<br/>

## 2) HTTP
수많은 프로토콜(통신규약)중 하나입니다. 우리는 이 HTTP를 이용해서 자원(Resource)를 요청하고 응답 할 수 있습니다.

<br/>

### HTTP_request
요청은 아래와 같은 경로를 통해서 이루어집니다.
```
http://127.0.0.1:3000/users/...
```

<br/>

### HTTP_Method
여러가지 http Method중 아래 4가지를 살펴보겠습니다.

| Method | 기능  |
|--------|-----|
| POST   | 생성  |
| GET    | 조회  |
| PUT    | 수정  |
| DELETE | 삭제  |

<br/>

### HTTP_response
- JSON, or XML
- status code

| status_code | 설명                    | 비고                     |
|-------------|-----------------------|------------------------|
| 200         | OK                    | GET                    |
| 201         | Created               | POST                   |
| 204         | No Content            | DELETE                 |
| 400         | Bad Request           | 잘못된 문법                 |
| 401         | Unauthorized          | 로그인 하지 않은 사용자가 개인정보 요청 |
| 404         | Not Found             | 없는 자원에 대한 요청           |
| 409         | Conflict              | 자원의 중복                 |
| 500         | Internal Server Error | 서버 에러                  |

<br/>

## 3) REST API
“Representational State Transfer” 의 약자이며, 자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 방법론 또는 규칙입니다.



### 특징 및 규칙
- Server-Client(서버-클라이언트 구조) *3세대 웹
- Stateless
- 경로에는 동사표현을 사용하지 않는다
- 자원은 명사형태로 표현한다
- 자원에 대한 행위는 HTTP_Method로 나타낸다