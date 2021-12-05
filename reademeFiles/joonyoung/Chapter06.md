# Debugging

## interactive debugging
1. break point 지정
2. Debugging 할 프로그램 지정(Node.js)
3. 재생버튼 -> 다음 break point로 넘아가기
4. Step over 코드 한줄한줄 내려가기
    - 함수를 호출하지는 않고 다음 라인으로 이동
5. Step into 함수 안까지 이동
6. Step out 함수 밖으로 이동

## Left panel
### Variable
1. 현재 선언 된 변수들의 값 확인
2. this의 값 확인
3. 실시간으로 직접 값 변경하면서 사용

### Watch
1. 내가 계속 확인 해보고 싶은것 등록
2. ex) `i === stop` ->  이렇게 해서 계속 값 확인

### Call stack
1. 어떠한 함수가 어떤 것을 호출했는지 확인

### Break point에 조건 부여
1. loop문에 break point를 지정하면 계속 몇번이고 확인 해야함
2. 조건을 부여하여 해당 조건에서만 break될 수 있도록 break의 조건 부여

## 자동재시작 Debugging
1. .vocode/launch.json 파일 생성
2. 스트립트 파일에 자동 재시작 조건 부여
```"runtimeExecutable" : "nodemon",
"restart" : true,
```