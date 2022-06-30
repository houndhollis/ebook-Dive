# 화살표 함수
> ES6 에서 도입된 화살표 함수는 function 키워드 대신 => 를 사용해 좀더 간략한 방법으로 함수를 선언할 수 있다. 화살표 함수는 항상 익명 함수로 정의한다

```
const add =(x,y) => x+y;
console.log(add(2,5)) // 7
```
화살표 함수는 생성자 함수로 사용할 수 없으며,기존 함쑤와 this 바인딩 방식이 다르고 prototype 프로퍼티가 없으며 argument를 생성하지 않는다.

## 함수 호출
- 함수는 함수를 가리키는 식별자와 한쌍의 소괄호인 함수 호출 연산자로 호출한다.

> 매개 변수는 함수 외부에서 참조할수 없고 내부에서만 참조가능하다
```
function add(x,y){
    console.log(x,y) // 2,5
    return x+y;
}
add(2,5);

console.log(x,y)// Error
```
- 인수가 부족해서 인수가 할당되지 않은 매개변수의 값은 undefined다.

```
function add(a = 0, b = 0,c = 0){
    return a+b+c;
}
console.log(add(1,2,3)) // 6
console.log(add(1,2)) // 3
console.log(add(1)) // 1
console.log(add()) // 0
```
이런식으로 없는값은 **기본값** 으로 설정할 수도있다.
- 이상적인 매개변수 개수는 0개이며 적을 수록 좋다.
- 이상적인 함수는 한가지 일만 해야 하며 가급적 작게 만들어야 한다.

## 반환문 
- 함수는 return 키워드와 표현식으로 이뤄진 반환문을 사용해 실행 결과를 함수 외부로 반환 할 수 있다.

```
function multiply(x,y){
    return x+y;
}
const result = multiply(3,5);
console.log(result);
```

- 반환문은 두가지 역할을 한다. 첫째, 반환문은 함수의 실행을 중단하고 함수 몸체를 빠져나간다.
- 반환문 이후에 다른문이 존재하면 그 문은 실행되지 않고 무시된다.
- 둘째, 반환문은 return 뒤에 오는 표현식을 평가해 반환한다.
- return 키워드 뒤에 반환값으로 사용할 표현식을 명시적으로 지정하지 않으면 undefined 가 반환된다. 

```
function foo(){
    return;
}
console.log(foo) // undefined
```
- 반환문은 생략할 수 있다. 이떄 함수는 함수 몸체의 마지막 문까지 실행한 후 암묵적으로 undefined 를 반환한다.

