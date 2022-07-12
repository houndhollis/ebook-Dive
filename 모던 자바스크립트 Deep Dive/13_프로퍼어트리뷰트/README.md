# 내부 슬롯과 내부 메서드

> 내부 슬롯과 내부 메서드의 개념에 대해 알아보자.
자바스크립트 엔진에서 실제로 동작하지만 개발자가 직접 접근할수 있도록 외부로 공개된 객체의 프로퍼티는 아니다 즉, 내부 슬롯과 내부 메서드는 자바스크립트 엔진의 내부 로직이므로 원칙적으로 자바스크립트는 내부 슬롯과 내부 메서드에 직접적으로 접근하거나 호출할 수 있는 방법을 제공하지 않는다.

## 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체
- 자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.
```
const person = {
    name:'woong'
}
// 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체를 반환한다.
console.log(Object.getOwnPropertyDescriptor(person,'woong'));
// {value : 'woong', writable:true, enumerable:true, configurable:true}
// 수정 , 갱신, 열거
```
Object.getOwnPropertyDescriptor 메서드를 호출할 때 첫 번째 매개변수에는 객체의 참조를 전달하고, 두 번째 매개변수에는 프로퍼티 키를 문자열로 전달한다. 이때 Object.getOwnPropertyDescriptor 메서드는 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체를 반환한다.

```
const person = {
    name:'woong'
};
person.age = 26;
// 프로퍼티 동적 생성

// 모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체들을 반환한다
console.log(Object.getOwnPropertyDescriptors(person));
{
    name: {value : 'woong' , writable:true, enumerable:true, configurable:true};
    age: {value :26 , writable:true, enumerable:true, configurable:true}
}
```

## 데이터 프로퍼티와 접근자 프로퍼티
- 프로퍼티는 데이터 프로퍼티와 접근자 프로퍼티로 구분할 수 있다.
1. 데이터 프로퍼티
키와 값으로 구성된 일반적인 프로퍼티다. 지금까지 살펴본 모든 프로퍼티는 데이터 프로퍼티다.
2. 접근자 프로퍼티
자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티다.

> 접근자 프로퍼티
1. get 
어트리뷰트[[Get]] 의 값, 즉 getter 함수가 호출되고 그 결과가 프로퍼티 값으로 반환된다.
2. set 
setter 함수가 호출되고 그 결과가 프로퍼티 값으로 저장된다.
- 접근자 함수는 getter/setter 함수라고도 부른다. 접근자 프로퍼티는 둘다 정의할수 있고 하나만 정의할수 있다.

```
const person = {
    firstName:'youngwoong'
    lastName:'Kim


// getter 함수
 get fullName(){
     return `${this.firstName} ${this.lastName}`
  },
// setter 함수
 set fullName(name){
     [this.firstName, this.lastName] = name.split(' ');
  },
};

// 데이터 프로퍼티를 통한 프로퍼티 값의 참조.
console.log(person.fistName+ ' ' + person.lastName); // youngwoong Kim

// 접근자 프로퍼티를 통한 프로퍼티 값의 저장
// 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
person.fullName = 'minwoo cho'
console.log(person); // {firstName : 'minwoo', lastName : 'cho'}

// 접근자 프로퍼티를 통한 프로퍼티 값의 참조
// 접근자 프로퍼티 fullName 에 접근하면 getter 함수가 호출된다.
console.log(person.fullName); // minwoo cho
```

person 객체의 firstName과 lastName 프로퍼티는 일반적인 데이터 프로퍼티다. 메서드 앞에 get set이 붙은 메서드가 있는데 이것들이 바로 getter와 setter 함수이다.
