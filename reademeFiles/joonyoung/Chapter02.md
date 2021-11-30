# Chapter02 What's Node.js

## 1. Node.js의 장점
- Javascript runtime
- Single thread
- Non-blocking I/o
- Event-driven

### Process VS Thread
- 둘다 실행단위이다.
- 프로세스는 운영체제로 부터 자원을 할당받는 작업의 단위
- 프로세스로 부터 자원을 할당받는 작업의 단위
- [프로세스 vs 스레드 참고영상](https://www.youtube.com/watch?v=1grtWKqTn50)

### Multy process
1. 하나의 프로세스가 잘못 되어도 프로그램은 잘 작동함
2. context switching이 발생함

### Multy thread
1. 시스템 자원 소모 감소, 처리 비용 감소, 쓰레드간 자원 공유
2. 디버깅이 어려움, 동기화의 이슈 발생

## 2. Node 서버
### 이벤트 루프
<image src="../src/image/event loop.png">

### Node app
- Main Single Thread
- Node.js APIs는 멀티스레드 제공(V8엔진을 사용하는데 V8엔진은 C++로 만들어 졌기 떄문)
- callback함수도 결국은 Main Single Thread에서 실행이 되어야 하는 함수이기 때문에 복잡한 일을 해서는 안된다.
- 단일 처리가 오래 걸리는 경우에는 Node로 서버를 구현하는것을 추천하지 않는다.
- 업무의 복잡도나 난이도가 높은경우 에러가 발생하면 서버가 죽기 떄문에 코드의 품질이 중요하다.

