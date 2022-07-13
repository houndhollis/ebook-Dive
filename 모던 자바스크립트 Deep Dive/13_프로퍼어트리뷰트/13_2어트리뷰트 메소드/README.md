# 프로퍼티 정의
> 프로퍼티 정의란?
- 새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 명시적으로 정의하거나, 기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의 하는 것을 말한다.
예를들어 프로퍼티 값을 갱신 가능하도록 할 것인지, 프로퍼티를 열거 가능하도록 할것인지 재정의 가능하도록 할것인지 할수있다.
- Object.defineProperty 메서드를 사용하면 프로퍼티의 어트리뷰트를 정의할 수 있다.
```
const person = {};
Object.defineProperty(person,'firstName',{
    value : 'woong',
    writable: true,
    enumerable : true,
    configurable: true,
});

Object.defineProperty(person,lastName,{
    value:'kim'
})
```
생략했을 경우 프로퍼티 디스크립터 객체에서 생략된 버트리뷰트는 기본값이 적용된다.
```
value : undefined
get : undefined
set : undefined
wirtable : false
enumerable : false
configurable : false
```
- Object.defineProperty 메서드는 한번에 하나의 프로퍼티만 정의할 수 있다.

## 객제 변경 방지
객체는 변경 가능한 값이므로 재할당 없이 직접 변경할 수 있다. 즉, 프로퍼티를 추가하거나 삭제할 수 있고, 프로퍼티 값을 갱신할 수 있으며, Object.definedProperty 또는 Object.defineProperties 메서드를 사용하여 프로퍼티 어트리뷰트를 재정의 할수도 있다.

- 객체 확장 금지 메서드: Object.preventExtensions 
프로퍼티 추가X , 삭제 값읽기 쓰기 재정의 O
- 객체 밀봉 메서드: Object.seal 
추가 삭제 재정의 X , 값읽기,쓰기 O
- 객체 동결 메서드: Object.freeze 
추가 삭제 값쓰기 재정의 X, 값 읽기 O

> 객체 확장 금지
Object.prevenExtensions 메서드는 객체의 확장을 금지한다. 객체 확장 금지란 프로퍼티 추가 금지를 의미한다. **확장이 금지된 객체는 프로퍼티 추가가 금지된다**

```
const person = {name:'woong'};

console.log(Object.isExtensible(person)); // true
```
- 확장이 가능한 객체인지 여부는 isExtensible 메서드로 확인가능하다.

> 객체 밀봉
Object.seal 메서드는 객체를 밀봉한다. 객체 밀봉이란 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지를 의미한다.**밀봉된 객체는 읽기와 쓰기만가능**

> 객체 동결
Object.freeze 메서드는 객체를 동결한다. 객체 동결이란 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지,프로퍼티 값 갱신 금지를 의미한다. **동결된 객체는 읽기만 가능하다**

## 불변 객체
지금까지 살펴본 변경 방지 메서드들은 얕은 변경 방지로 직속 프로퍼티만 변경이 방치되고 중첩 객체까지는 영향을 주지 못한다.
