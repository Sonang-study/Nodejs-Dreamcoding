## 10. RESTful API
*Representational State Transfer*
*상태를 나타내는 전송* 

::Architectural Styles and Design of Network-based Software Architectures::

### RESTful API를 만들기 위해 지켜야 하는 6가지 원칙

*API : Application Programming Interface*
*REST : Representational state Transfer (무언가를 대표하는 상태를 전송)*
-> Software Architectural Style, Web Service Guideline

1. ::Client-server architecture::
2. ::Statelessness:: 
(다른요청과 연결되면 안됨)  <HTTP>
3. ::Cacheability::  <HTTP>
4. ::Layered System:: 
(공통된 API 하나로 서버가 얼마나 있는지 상관없이)
5. ::Code on demand::
6. ::Uniform interface::
- Resource Identification in requests
클라이언트가 이해할 수 있는 형태로 데이터를 보내준다
- Resource manipulation through representations
해당 리소스를 어떻게 처리할 수 있는 지를 알 수 있어야 한다
- self-descriptive messages (어떻게 client가 처리해야하는지 명시 되어있어야함)
데이터 안에 JSON을 PARSING 해야되는 지 등을 알려줘야 한다.
- Hypermedia as the engine of application state (HATEOAS)
 서버로 부터 받은 URL 을 통해서 어떻게 서버를 이용하면 되는지 알 수 있다.

-> URL 뿐만아니라 HyperLink도 잘 제공해야 한다.

### API 디자인 하는 방법 (CRUD)
Create : POST
Read : GET**
Update : PUT
Delete : DELETE 를 이용하여 만든다.

Verb / What
GET / posts
POST /posts
GET /posts/1  PUT /posts.1  DELETE /posts/1 와 같이 ::동사 /무엇을::  로 작성
GET / tags/?postId=1 ::무엇을:: 원하는지 정확하게 작성



## 11. Express.js의 사용방법
### Why Express?

1. 많은 사람들이 사용하는 Library
2. 하나의 Framework를 배우기에 굉장히 간단하다

### Express.js 사용법
[Express 4.x - API Reference](https://expressjs.com/en/4x/api.html)

```javascript
const express =require("express")
const app=express()

app.get('/psts',function(req,res,next){
	res.send(...)
}

app.post('/posts',function(req,res,next){
	res.send(...)
}

app.listen(8080);
```

-> 수많은 미들웨어의 체인으로 연결되어있다.
(한번 response를 보내면 뒤 middleware는 처리되지 않음)

- app.all과 app.use의 차이점?
app.all : 정해진  url에 한해서만 적용
app.use : 정해진 url에 추가 params/ query까지 있어도 상관없음

- 콜백함수 안에서 쓸때는 response는 한번만 사용하거나 사용한 후 콜백함수 에서 나갈 수 있도록 한다.

- express.json()은 자동으로 json을 parsing 하는 기능

### 서버에서 에러처리하기
1. 적절한 ::에러메시지:: 를 보내줄 것
2. 서버가 중지 되지 않도록, 에러에서 빠르게 복귀될 수 있도록 ::예외처리::를 할 것

### 동기, 비동기
동기 : promise
비동기 : async 가 어떤게 다를 것인가?
유투브를 보고와라!

### 유툽 Javascript  Dreamcoding
- async 와 defer의 차이점
1. head의 script에 넣는법
script 크기가 크면 로딩이 늦어진다
3. body의 끝부분에 script하는 법
JS에 의존적이라면 fetching과 excuting을 모두 기다려야한다.
3. async를 이용해 병렬적으로 이용한다.
queryselector를 이용할 경우 HTML이 아직 만들어지지 않았을 수 있다.
순서에 상관없이 다운로드 받아지는 대로 실행된다.
4. defer을 이용
parsing하는 동안 다 다운받고 이어서 html을 excute한다.
실행 시에도 순서대로 실행한다.

- JSON 개념정리
*JavaScript Object Notation*
Object  -> Serialize -> string
String -> deserialize -> Object
1. Object to JSON
JSON.stringify 이용
```javascript
let json = JSON.stringify(['apple', 'banana']);
// ["apple", "banana"]
console.log(json)

const rabbit ={
	name: "tori",
	color: "white",
	size: null,
	birthDate: new Date(),
	symbol: Symbol('id'),
	jump: ()=>{
		console.log(`${name} can jump!`);
	}
}
json = JSON.stringify(rabbit);
console.log(json);
// {""name":"tori","color":"white","size":json.null, "birthDate":"2020-05-29T13:20:22.670Z"}

```

-> 함수 및 Symbol은 제외된다.
(원하는 property만 replacer에 전달하여 원하는 property만 json화 시킬 수 있다. 혹은 callback 함수를 통해 세밀하게 통제)

2. JSON to Object
JSON.parse
```javascript
json= JSON.stringify(rabbit);
const obj=JSON.parse(json);
console.log(obj);
//
rabbit.jump();
//함수는  json화 되지 않았기 때문에 다시 찾아올 수 없다.
console.log(rabbit.birthDate.getDate());
//29
console.log(obj.birthDate.getDate());
//Error obj.birthDate는 이제 그냥 String이 obj에 할당된 것이다.

const obj JSON.parse(json, key,value)=>{
	return key ==='brithdate' ? new Date(value) : value
}
console.log(obj.birthDate.getDate())
//29
```
- 콜백 이해하기
-
JavaScript is synchronous
Execute the code block by order after hoisting
hoisting: var, function declaration
-> 변수 또는 함수들이 런타임 전에 먼저 선언되는 것을 말한다.

```javascript
//Synchronous callback
function printImmediately(print){
	print();
}
printImmediately(()=> console.log("hello"));

//Asynchronous callback
function printWithDelay(print,timeout){
	setTimeout(print, timeout);
}
printWithDelay(()=> console.log("async callback"), 2000);


//Callback Hell example
class UserStorage {
	loginUser(id, password, onSuccess, onError){
		setTimeout(()=>{
		if((id === "ellie" && password === "dream") ||
		   (id === "coder" && password === "academy")
		){
			onSuccess(id);
		}else{
			onError(new Error('not found'));
		}
		}, 2000)
	}
	getRoles(user, onSuccess, onError){
		setTimeout(()=>{
			if(user === "ellie"){
				onSuccess({ name: "ellie", role: "admin"});
			} else{
				onError(new Error("no access"));
			}
		}, 1000)
	}
}
```


- 프로미스 개념부터 활용까지
-> 프로미스는 비동기 함수이며 콜백지옥에서 벗어나게 해주는 해결 방안이다
이 때 async /await이 함수를 더 간단하게 만들 수 있도록 해준다.
async는 new Promise((resolve,reject)=>{})에서 return이 resolve로 동작하는 것처럼 해준다. await은 비동기 함수를 동기적으로 실행이 다끝나고 난 뒤 다음 줄이 시작할 수 있도록 동작한다.

- 에러제어
1. 동기함수 -> try{}catch{}를 통해 에러를 제어할 수 있다.
2. 비동기 함수 -> then으로 성공했을 때 catch를 통해 에러가 있을 때를 제어한다. 에러가 밖으로 던져지지 않기 때문에 try--catch를 사용할 수 없다.
3. async await -> 비동기함수 이지만 try--catch를 사용할 수 있다.

express-async-errors를 통해 비동기 함수도 맨 밑의 error controller에서 걸려서 에러가 발생할 수 있도록 한다.

