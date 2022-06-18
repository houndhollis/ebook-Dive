# 7_2 객체 작성!

> 식별자 네이밍 규칙을 따르지않으면?
- 큰일난다. 밑에 코드를 본다면

```
const person = {
    firstName = 'youngwoong',
    last-name = 'kim', // SyntaxError: Unexpected token - 
}; 
```
- 프로퍼티 키는 식별자 네이밍 규칙을 준수해야 한다. 
- last-name 은 식별자 규칙을 준수하지 않았다, 자바스크립트는 -를 연산자가 있는 표현식으로 해석한다.

문자열 또는 문자열로 평가할 수 있는 표현식을 사용해 프로퍼티 키를 동적으로 생성할 수도 있다. 이 경우에는 프로퍼티 키로 사용할 표현식을 대괄호([..]) 로 묶어야 한다.

## 메서드 
- 자바스크립트 에서 사용할수 있는 모든 값은 프로퍼티 값으로 사용할수 있다.
- 함수는 일급객체 이므로 값으로 취급할 수 있다.
- 프로퍼티 값이 함수일 경우 일반함수와 구분하기 위해 메서드 라 부른다.

``` 
const circle = {
    radius:5, // 프로퍼티   
    getDiameter: function(){ //지름 구하기, 메서드
        return 2 * this.radius;
    }
};
console.log(circle.getDiameter()) // 10
```

- 메서드 내부에서 사용한 this 키워드는 객체 자신을 가리키는 **참조 변수** 다

## 프로퍼티 접근
- 프로퍼티 접근 방법은 두가지다
1. 마침표 표기법 dot notation
2. 대괄호 표기법 bracke notation

```
const person = {
    name : 'woong',
};

console.log(person.name) // 마침표 표기법에 의한 프로퍼티 접근
console.log(person['name']) // 대괄호 표기법에 의한 프로퍼티 접근
```
- 대괄호 표기법을 사용하는 경우 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 **따옴표로 감싼 문자열**이여야 한다.

