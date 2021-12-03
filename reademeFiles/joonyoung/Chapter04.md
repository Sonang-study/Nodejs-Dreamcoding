# Chapter04 Node Module

## 1. Global object
- 브라우저 환경에서는 window가 global객체
- Node환경에서는 global이 global객체
- global에 있는 내용을 가져다가 쓰는 경우는 많으나 우리가 직접 global에 변수를 정의해서 사용하는 일은 없다.
- [Node global 참조문서](https://nodejs.org/dist/latest-v16.x/docs/api/globals.html)

## 2. 콘솔 로그
- log : 개발
- info : 정보전달
- warn : 경보
- error : 심각한 에러, 사용자 에러, 시스템 에러
- time : 시작과 끝점 걸린 시간 확인(품질 확인)
- trace : 어디서 어떤 함수가 불렸는지 확인 가능

## 3. This
- 어떤 환경에서 돌리느냐에 따라서 다르다
- 어떤 위치에서 this를 호출하느냐에 따라서도 다르다

## 4. import, export
### export
```javascript
//./counter.js
function increase() {
    return count
}

function getCount() {
    return count
}

module.exports.getCount = getCount // module.exports.get = getCount 이렇게도 가능
module.exports.increase = increase

//또는
module.exports = {
    getCount : getCount,
    increase : increase
}
```

### import
```javascript
const counter = require('./counter.js')

counter.increase();
counter.getCount();
```

## 5. import, export with ES6
```json
//package.json
"type" : "module"
```
### export
```javascript
export function increase() {
    return count
}

export function getCount() {
    return count
}
```
### import
```javascript
import {increase, getCount} from './counter.js';
```
## 6. process
```javascript
const process = require('process');

process.nextTick(() => {
    //something
})
//process.nextTick의 기능은 callback queue의 우선순위를 1순위로 만들어 준다.
```

## 7. path
```javascript
const path = require('path');

console.log(__dirname); // 현재 코드가 돌아가고 있는 파일의 위치
console.log(__filename); // 현재 코드의  파일의 경로포함 파일의 이름

// 운영체제가 다르면 경로 표기법이 다르기 때문에 우리가 직접 경로를 지정해주면 안되고 위와 같은 기능을 사용해야 한다.

//path.sep => 경로 구분자

//path.delimiter => 환경변수 구분자

//path.basename(__filename) => 파일의 이름 + 확장자

//path.basename(__filename, '.js') => 파일의 이름의 확장자 제거 기능

//path.parse(__filename) => 파일의 정보 구분해서 obj형태로 반환
```

## 8. 버퍼와 스트림
> 파일을 한번에 전체를 읽어와서 사용하면 메모리의 낭비가 있다.
파일을 다 읽는데 이때 내 메모리보다 큰 파일을 읽게되면 문제가 발생할 수 있다.
이러한 문제를 해결하는데 stream을 활용하면 좋다. 조금씩 읽고 쓰고를 반복할 수 있다.

### 스트림 방법
```javascript
const fs = require('fs'); //fs class 참조

const readStream = fs.createReadStream('./file.txt', {
  //   highWaterMark: 8, // 64 kbytes가 기본 사이즈 // 데이터를 자를 크기
  //   encoding: 'utf-8', // 인코딩 타입
});

const beforeMem = process.memoryUsage().rss; // 메모리 사용량 체크하기 위한 것
const data = [];
readStream.on('data', (chunk) => {// .once를 사용하면 한번만 일어난다.
  // console.log(chunk);
  data.push(chunk);
  console.count('data');
  readStream.close();
});// 조각 한 조각만 잘라서 읽고 출력하고 Stream 그만두기

readStream.on('close', () => {
  console.log(data.join(''));
  // calculate
  const afterMem = process.memoryUsage().rss;
  const diff = afterMem - beforeMem;
  const consumed = diff / 1024 / 1024;
  console.log(diff);
  console.log(`Consumed Memory: ${consumed}MB`);
});
readStream.on('error', (error) => {
  console.log(error);
});
```

## 9. 파이프의 사용
### 예제
```javascript
const readStream = fs.createReadStream('./file.txt');
const zlibStream = zlib.createGzip();
const writeStream = fs.createWriteStream('./file4.zip');
readStream.pipe(zlibStream).pipe(writeStream) // 읽기, 압축, 쓰기가 한 세트 사이클 단위로 돌아감.
.on('finish', () => {
  console.log('done!!');
});
```

## 10. 이벤트
> 이벤트 클래스는 사실상 우리가 만들어서 사용할 일은 크게 많지 않다. JS내부적으로 동작하는 기능이 많다.

### 예제
```javascript
const EventEmitter = require('events');
const emitter = new EventEmitter();

const callback1 = (args) => {
  console.log('first callback - ', args);
};
emitter.on('ellie', callback1); // ellie라는 이벤트 리스너 등록 및 이벤트 발생 시 실행할 함수 등록

emitter.on('ellie', (args) => {
  console.log('second callback - ', args);
});

emitter.emit('ellie', { message: 1 }); // 이벤트 발생 시키기 및 변수 전달
emitter.emit('ellie', { message: 2 });
emitter.removeAllListeners();
emitter.emit('ellie', { message: 3 });
```