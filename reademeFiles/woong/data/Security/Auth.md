**Open Web Application Security Project**
web에서 빈번하게 일어나는 이슈 10가지 [OWASP 10](https://owasp.org)


# XSS Attack
Cross Site Scripting Attack

> 문제점 : 현재 웹에서는 localstorage에 token을 저장 해 놨다.
> Javascript를 몰래 페이지에 숨겨 놓고, 사용자가 이용하는 도중 cookie와 
> localstorage의 정보를 읽어와서 Hacker에게 보낸다.
> 따라서 민감한 정보는 cache, localstorage에 저장하지 않는다.
> 1. Memory 상에 보관한다.
> 2. HTTP ONLY 옵션으로 cookie사용(모바일 클라이언트에서는 사용할 수 없다 CSRF attack에 취약하다.)
> 
**example**
[googleExample](https://www.google.com/about/appsecurity/learning/xss/)

서버에서 httponly옵션을 이용해서 header에서 온 token을 저장 할 수 있음.

# CSRF
currently authenticated된 사용자의 session에 session riding 하여 무엇인가 하는 옵션

방지법: CSRF token(메모리에 저장)을 모든 요청에서 사용

1. Secure frontend
2. Compatible Backend

# Rate Limiter 
서버에 과부하를 방지
ex. Business Products(apigee, tykio) , Cloud Services(AWS API Gateway, Google Cloud API Gateway)