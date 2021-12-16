# JS this 키워드

## this의 필요성
-> 메서드가 자신이 속한 객체의 프로퍼티를 참조하고 변경할 수 있게 하기 위해서 필요
*호출방법*
> 1. 자신이 속한 객체를 재귀적으로 호출
> 2. 생성자 방식으로 호출
> 3. this를 통한 호출
```Javascript
 const circle = {
radius:5,
getDiameter() {
return 2 * circle.radius;
	}
};
console.log(circle.getDiameter()); //10

function Circle(radius) {
	???.radius = radius;
}
Circle.prototype.getDiameter = function () {
	return 2 * ???.radius;
};

const circle = new Circle(5);

//두 방법 모두 일반적이지도 않고, 바람직 하지 않다
``` 

## this 바인딩
-> this 가 가리키는 값 this 바인딩은 함수 호출방식에 의해 동적으로 결정된다.
(바인딩: 식별자와 값을 연결하는 과정)

> 1. 일반함수 내부에서 호출 -> window가 바인딩(콜백함수로 호출할 때는 일반함수와 동일)
> * use strict 모드일때는 undefined로 출력
> 2. Method 내부에서 호출 ->  method를 호출한 객체와 바인딩
> 3. 생성자 함수 내부에서 호출 -> 생성자 함수가 생성할 인스턴스와 바인딩
> 4. Function property로 호출 -> 지시되어 있는 객체와 바인딩
> 5. 화살표 함수로 호출 -> 상위 스코프의 this를 호출

-> 대부분 화살표 함수를 호출하여 많이 사용

```javascript
var value = 1;

const obj ={
	value:100,
	foo(){
		setTimeout(()=>console.lopg(this.value), 100); //100
	}
}

obj.foo();
```
