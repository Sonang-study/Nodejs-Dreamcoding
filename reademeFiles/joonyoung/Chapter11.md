# Chapter11
## Express 시작하기
::Express::
시작하기
[Express 공식문서]([Express 4.x - API Reference](https://expressjs.com/en/4x/api.html))
1. Npm init —yes (default값으로 설정된 package.json을 만들겠다)
2. Npm I express
3. Package.json 수정 // “start” : “nodemon app”
4. Npm I nodemon —save-dev -> 다른 개발자들이 이거 가져가서 npm I 할 때 자동으로 설치
	* `npm install` -> will install both “dependencies“ and “dev Dependencies”
	* `npm install —production`  -> will only install “dependencies“
	* `npm install —dev`  -> will only install “dev Dependencies“
5. “type” : “module” -> use ES6
6. App.js 생성
```javascript
import express from 'express'
const app = express();

//app.all 은 모든 Http Method에 대해 처리 가능
//app.use는 all과는 조금 다르지만 일단은 모든 Http Method 처리 가능
app.get('/', (req, res, next) => {
	console.log('get');
	res.send("something");
});

app.listen(8080);
```
7. Npm start

## Req
Path, headers, params, query 이렇게 다 받을 수 있음

## Res
send로 데이터 보내기 가능
Res.json({name : “jayko”}) 이렇게도 가능
res.status(200).send(“message”) 가능
Res.setHeader(“key”, “value”) <- 이런 형식으로 보내야 함

## Middleware의 특징
> callback 함수는 누가 먼저 등록했는지가 정말 중요하다
### EX1
```javascript
import express from 'express'
const app = express();

app.get('/', (req, res, next) => {
	console.log('first');
},
(req, res, next) => {
	console.log('first2');
});

app.get('/', (req, res, next) => {
	console.log('second');
});

app.listen(8080);
```

### 결과 값
```bash
first
```
경로가 / 로 일치하여 제일 처음의 middleware가 호출이 되었는데, 
우리가 res(응답)하거나 next(다음 함수로 연결) 무언가 해주어야 하는데, 안해주면 서버가 중지 된 상태가 된다.

### EX2
```javascript
import express from 'express'
const app = express();

app.get('/', (req, res, next) => {
	console.log('first');
	next();
},
(req, res, next) => {
	console.log('first2');
});

app.get('/', (req, res, next) => {
	console.log('second');
});

app.listen(8080);
```

### 결과 값
```bash
first
first2
```

### EX3
```javascript
import express from 'express'
const app = express();

app.get('/', (req, res, next) => {
	console.log('first');
	next('route');
},
(req, res, next) => {
	console.log('first2');
});

app.get('/', (req, res, next) => {
	console.log('second');
});

app.listen(8080);
```

### 결과 값
```bash
first
second
```
`next('route’)` 해주면 같은 라우터 안에 있는 first2는 무시되고 second로 간다
같은 경로에 여러개의 Middleware가 연결되어 있다면, 처음으로 응답이 일어나면 동일한 경로의 다른 응답들은 이루어질 수 없음

```javascript
app.use((req, res, next) => {
	res.status(404).send('Page Not Found');
});
//위에서 내가 처리해줄 경로는 다 처리해주는데 거기에 안결렸으면 우리가 의도한 경로가 아니란 이야기니까 위의 방식대로 예외처리를 해주어야 함

app.use((error, req, res, next) => {
	console.log(error);
	res.status(500).send('sorry server have matter');
});
//위의 방식으로 error처리를 해주어야 함
```

::app.all() vs app.use()::
```javascript
app.all('/api', (req, res, next) => {
console.log("api");
next();
});
//모든 Http Method에 대해서 처리 가능
//하지만 오로지 /api 경로에서만 가능 /api/xxx/xxx는 안됨

app.use('/sky', (req, res, next) => {
console.log("use");
next();
});
//해당 경로 포함해서 뒤에 어떠한 것이 붙던지 괜찮아 /sky/xx/xxxx 가능
```

*If문으로 분기처리 해주고 싶을 때*
Return res.send를 해주어야지 그냥 res.send 해주면 안됨
하나의 callback함수에서는 하나의 res.send만 허용한다.