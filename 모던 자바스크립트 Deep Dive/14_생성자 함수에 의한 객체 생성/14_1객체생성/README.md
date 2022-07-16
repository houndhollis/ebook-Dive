# 17_1 객체 생성

객체 리터럴 에서 객체 리터럴에 의한 객체 생성방식을 살펴보았다. 객체 리터럴에 의한 객체 생성 방식은 가장 일반적이고 간단한 객체 생성방식이다 이번에는 생성자 함수를 이용해서 객체를 생성하는 방식을 살펴본다.

## Object 생성자 함수
- new 연산자와 함께 Object 생성자 함수를 호출하려면 빈 객체를 생성하여 반환한다. 빈 객체를 생성한 이후 프로퍼티 또는 메서드를 추가하여 객체를 완성할 수 있다.

```
const person = new Object();

//프로퍼티 추가
person.name = 'woong'
person.sayHello = function(){
    console.log('Hi hello' + this.name);
};

console.log(person) // {name:'woong',sayHello}
person.sayHello() // Hi hello woong
```

생성자 함수 란 new 연산자와 함꼐 호출하여 객체를 생성하는 함수를 말한다. 생성자 함수에 의해 생성된 객체를**인스턴스** 라고 한다.

## 생성자 함수
- 객체 리터럴에 의한 객체 생성 방식은 직관적이고 간편하다. 
하지만 객체 리터럴에 의한 객체 생성 방식은 단 하나의 객체만 생성한다. 따라서 동일한 프로퍼티를 갖는 객체를 여러 개 생성해야 하는 경우 매번 같은 프로퍼티를 기술 해야 하기떄문에 비효율이다
```
function Circle(radius){
    // 생성자 함수 내부의 this 는 생성자 함수가 생성할 인스턴스를 가리킨다.
    this.radius = radius;
    this.getDiameter = function(){
        return 2 * this.radius;
    };
}

// 인스턴스 생성
const circle1 = new Circle(5) // 반지름 5
const circle2 = new Circle(10) // 반지름 10
```
- 이런식으로 객체 리터럴 보다 효율적으로 중복 메소드를 생성자 함수로 처리할 수가있다.

> this
this 는 객체 자신의 프로퍼티나 메소드를 참조하기 위한 **자기 참조 변수**다. this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 따라 동적으로 결정된다.

- 함수 호출 방식 -> this가 가리키는 값(this 바인딩)
-  일반 함수로서 호출 -> 전역객체
-  메서드로서 호출 -> 메서드를 호출한 객체(마침표 앞의 객체)

```
// 함수는 다양한 방식으로 호출될 수 있다.
function foo(){
    console.log(this)
}
// 일반적인 함수로서 호출
// 전역 객체 브라우저 환경에서는 window, Node.js 환경에서는 global을 가리킨다.
foo(); // window

const obj = { foo }; // ES6 프로퍼티 축약 표현

// 메서드로서 호출
obj.foo() // obj

// 생성자 함수로서 호출
const inst = new foo(); // inst
```
생성자 함수는 일반 함수와 동일한 방법으로 생성자 함수를 정의하고 new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다.

## 생성자 함수의 인스턴스 생성 과정
생성자 함수는 인스턴스를 생성하는 것과 생성된 인스턴스를 초기화(인스턴스 프로퍼티 추가 및 초기화 할당 ) 하는 것이다. 생성자 함수가 인스턴스를 생성하는 것은 필수이고, 생성된 인스턴스를 초기화하는 것은 옵션이다.
```
function Circle(radius){
    //인스턴스 초기화
    this.radius = radius;
    this.getDiameter = function () {
        return 2 * this.radius
    }
}

const circle1 = new Circle(5); //반지름이 5인 객체 생성
```
## 인스턴스 생성과 this 바인딩
암묵적으로 빈 객체가 생성된다. 이 번 객체가 바로 생성자 함수가 생성한 인스턴스다.  암묵적으로 생성된 빈 객체, 즉 인스턴스는 this에 바인딩 된다. 생성자 함수 내부의 this가 생성자 함수가 생성할 인스턴스르 가리키는 이유가 바로 이것이다.

``` 
function Circle(radius){
    // .1암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
    console.log(this); //Cicle {}

    this.radius = radius;
    this.getDiameter = function(){
        return 2*this.radius;
    };
}
```

> 인스턴스 초기화
- 생성자 함수에 기술되어 있는 코드가 한 줄씩 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다. this 에 바인딩되어 있는 인스턴스에 프로퍼티나 메서드를 추가하고 생성자 함수가 인수로 전달받은 초기값을 인스턴스 프로퍼티에 할당하여 초기화하거나 고정값을 할당한다.

