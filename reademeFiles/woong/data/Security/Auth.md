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
서버에 과부하를 방지, balanced Use, Differentiate Level of Service

-> Load balancer를 이용!, Redis Store가 Server 뒷 단에서 계산중이다.
ex. Business Products(apigee, tykio) , Cloud Services(AWS API Gateway, Google Cloud API Gateway)

대표적인 알고리즘 4가지(미리 알아두면 도움이 될)

1. Fixed window: 특정한 기간동안에만 request를 받는 것
    (특정 시간에 갑자기 많은 요청이 들어올 수 있다.)
2. Sliding window: 요청이 들어오는 시간대 앞 뒤로 부하를 계산하는 것
3. Leaky bucket(양동이와 조그만 구멍) : 큐 자료구조 이용
 -> 동시다발적으로 많은 접속이 발생할 수 있는 서비스는 X
4. Token bucket: 큐 자료구조 이용
 -> 버킷안에 있는 동전을 주워서 요청을 처리

# Client side considerations(429)

몇 초 뒤에 retry하면 되는 지를 같이 보내주기 때문에
점진적으로 늘려가면서 요청을 한다. 단 , Jitter를 이용해서!