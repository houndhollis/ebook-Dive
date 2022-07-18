# 객체생성_인스턴스 반환
- 생성자 함수 내부의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.

```
function Circle(radius){
    // 1. 암묵적으로 빈 객체가 생성되고 this에 바인딩 된다.

    // 2. this에 바인딩되어 있는 있는 인스턴스를 초기화 한다.
    this.radius = radius;
    this.getDiameter = function () {
        return 2 * this.radius
    };
    // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
}

// 인스턴스 생성. Circle 생성자 함수는 암묵적으로 this를 반환한다.
const circle = new Circle(1);
console.log(circle); // Circle {radius: 1, getDiameter: f}
```

만약 this가 아닌 다른 객체를 명시적으로 반환하면 this가 반환되지 못하고 retrun 문에 명시한 객체가 반환된다.

```
function Circle(radius){
    // 1. 암묵적으로 빈 객체가 생성되고 this에 바인딩된다.

    // 2. this에 바인딩되어 있는 인스턴스를 초기화 한다.
    this.radius = radius;
    this.getDiameter = function () {
        return 2 * this.radius;
    };
    // 3. 암묵적으로 this를 반환한다.
    // 명시적으로 객체를 반환하면 암묵적인 this 반환이 무시된다.
    return {}
}

// 인스턴스 생성 Circle 생성자 함수는 명시적으로 반환한 객체를 반환한다.
const circle = new Circle(1);
console.log(circle) // {}
```
- 하지만 명시적으로 원시값을 반환하면 원시 값 반환은 무시되고 암묵적으로 this가 반환된다
예를 들어 마지막에 return {} 가 아닌 return 100을 했을 경우 콘솔에 찍을 때 파라미터로 입력한 값이 출력된다.

## 내부 메서드 [[Call]]과 [[Construct]]
함수 선언문 표현식으로 정의된 함수는 일반적인 함수로서 호출할 수 있는 것은 물론 생성자 함수로서 호출할수 있고 생성자 함수로 호출한다는 것은 new 연산자와 함께 호출하여 객체를 생성하는 것이다.

```

// 함수는 객체다

function foo(){}

// 함수는 객체이므로 프로퍼티를 소유할 수 있다.
foo.prop = 10;

// 함수는 객체이므로 메서드를 소유할 수 있다.
foo.method = function () {
    console.log(this.prop);
}

foo.method(); // 10
```
- 함수는 객체이지만 일반 객체와 다르다. **일반 객체는 호출이 안되지만 함수는 호출 가능하다** 따라서 함수는 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드를 가지고 있다.

```
function foo(){}
// 일반적인 함수로서 호출: [[Call]] 이 호출된다.
foo()

// 생성자 함수로서 호출: [[Construct]]가 호출된다.
new foo();
```
## constructor 와 non-constructor의 구분

- constructor : 함수 선언문, 함수 표현식, 클래스(클래스도 함수다)
- non-constructor: 메서드,화살표 함수

```
// 일반함수 정의: 선언문, 표현식
function foo(){}
const bar = function () {};

// 프로퍼티 x의 값으로 할당된 것은 일반함수로 정의된 함수다. 이는 메서드로 인정하지 않는다
const baz = {
    x : function (){}
};

// 일반 함수로 정의된 함수만이 constructor 다.
new foo(); // -> foo{}
new bar(); // -> bar{}
-----------------------
new baz.x(); // -> x {}

// 화살표 함수 정의
const arrow = () => {};

new arrow(); // TypeError: arrow is not a constructor

// 메서드 정의: ES6의 메서드 축약 표현만 메서드로 인정한다.
const obj = {
    x(){}
};

new obj.x(); // TypeError: obj.x is not a constructor
```
함수롤 프로퍼티 값으로 사용하면 일반적으로 메서드로 통칭한다 **하지만** ECMAScript 사양에서 메서드란 ES6의 메서드 축약 표현만 의미한다. 다시 말해 함수가 어디에 할당되어 있는지에 따라 메서드인지를 판단하는 것이 아니라 함수 정의 방식에 따라 constructor와 non-constructor 를 구분한다.
