
## 1. Introduction
## 2.  Node의 전반적인 개념(What's Node JS?)

### 노드는 무엇이고 어떻게 공부하는게 좋을까?
 JavaScriptCord, Chakra SpiderMonkey V8(JIT, Just in time Engine) -> JavaScript Engine(1995)

Ryan Dahl : 자바스크립트로 모든걸 다할 수 있으면 ?
Backend & Server, Front0end, Scripting&Automation 모두 가능!!

Front-end Knowledge(Web API들을 공부하고 확장한다) -> Vue, React(프레임워크)
Back0end (Node.js API에 대해서 공부해야 한다) -> Express, Nest(프레임워크)
::Browser와 같은 존재가 바로 NodeJS이다:: 

### 왜 노드를 배워야 할까?

- ::JavaScript를 통해 모든 것을 할 수 있다. (프론트와 백을 모두 할 수 있다.)::
- Context-Switching이 필요 없다. C(JS), S(Java)로 하는 경우
- 개발자의 생산성이 올라감(상대적으로 쉽게 full-stack이 될 수 있다.)
- Prototype을 빠르게 만들 수 있다.
- ::절반이 상의 개발자가 Node.js를 사용가능:: 
- ::큰 기업들도 이용하고 있다.::
-> 강력한 커뮤니티가 존재한다.
-> Production quality를 보장한다.
-> 많은 Tool들이 이미 다 존재한다.
- ::쉽고 심플하지만 powerful, flexible한 언어이다:: 
- ::Strong Community::(NPM, Node Package Manager)

### Node의 4가지 특징

1. JavaScript Runtime
2. Single Thread
> process 와 Thread의 차이는?
> 프로그램을 여러개 띄우는 것은 이것 저것 왔다갔다하면서 쓰는 것임 Reasource(Code, stack, Heap, data의 구성)
> 기능마다 Thread들이 존재한다. Process내부에서 Thread를 시간을 할당하여서 하나하나 처리한다.
> Thread 많아지면, 비용증가, 등 마냥 좋지만은 않다(concurrency API -> Java)
> 하나의 일이 끝날 때 까지 기다렸다가 다음 것을 진행하는 동기적인 언어가 JS이다.
3. Non-Blocking I/O
> I/O(Input, Output) vs CPU(두뇌),
> Blocking : 하나가 끝나면 다음, 동기적으로 진행 되는 것
> Non-Blokcing : asynchronous한 것 콜백을 던졎주고 다음으로 넘어간다.
4. Event-Driven (이벤트를 호출 할  수 있다.)

Node JS는 Call Stack을 가지고 있다.
EventLoop가 CallStack과 Task Queu를 비교, Callstack이 비었을때 Task Queu에서 불러움
NodeJS 내부에서는 Multi Thread가 가능하다. 외부는 Main Single Thread 이다. 

효율적인 I/O방식, 무거운일을 하는 CPU에는 별로다 
NodeJS 12에서는 worker thread를 통해 <Multi thread달성 가

### 노드서버와 일반 서버의 차이점

Thread Pool의 개수만큼 한번에 처리 가능, 개수를 넘으면 대기

노드서버는 여러가지 요청을 빠르게 처리 가능(주문을 받는 점원이 따로 있다.)

## 3. Tools. Preparation
### REPL이란 무엇인가

Read Eval Print Loop (정보를 받아서 연산 프린트 반복)

### 노드 파일로 실행해 보기

node  파일이름 -> 실행가능

## 4. Node Modules

### Node 모듈을 어디서 찾아야하는지

### 4.3 글로벌 오브젝트 - 소스 공부법

WebBrowser 에서는 windows와 같은 것이 Node 에서의 global 전역 객체로 활용된다


## 4.11 path 그리고 유의할 점

## 4.14 Buffer와 스트림
- progressive Download
- Twitch를 실시간 방송할 때 쓰는 기법이다. 
- -> Node에서는 어떻게 이용할 수 있을까?

