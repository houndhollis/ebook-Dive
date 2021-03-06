# 9_4 재귀함수
> 재귀함수란?
- 함수가 자기 자신을 호출하는 것을 재귀 호출 이라 한다. 재귀 함수는 자기 자신을 호출하는 행위, 즉 재귀 호출을 수행하는 함수를 말한다.
- 재귀 함수는 반복되는 처리를 위해 사용한다.

```
function countDown(n){
  for(let i = n, i >= 0; i--){
      console.log(i)
  }
}

countDown(10)
```
위에 함수는 문제 없이 잘 작동한다 그러나 반복문 없이 구현할 수 있는 방법이 있다.
```
function countDown2(n){
    if(n<0){
    return;
    }
    console.log(n)
    countDown2(n-1)
}
countDown2(10)
```
- 재귀 함수를 사용하면 반복되는 처리를 반복문 없이 구현할수 있다.
팩토리얼은 재귀함수로 간단히 구현 가능하다
```
function factorial(n){
    if(n <= 1) return 1;
    return n*factorial(n-1);
}
5! = 120
```
팩토리얼 함수 내부에서 자기 자신을 호출할 때 사용한 식별자는 함수 이름이다 함수 이름은 함수 몸체 내부에서만 유효하다 따라서 자기자신을 호출할 수 있다. 함수 표현식으로 정의한 함수 내부에서는 함수 이름은 물론 함수를 가리키는 식별자로도 자기 자신을 재귀 호출할 수 있다.
- 재귀 함수는 자신을 무한 재귀 호출한다 따라서 재귀 함수 내에는 재귀 호출을 멈출수 있는 **탈출조건**을 반드시 만들어야 한다. 탈출 조건이 없으면 함수가 무한 호출되어 **스택 오버플로** 에러가 발생한다

## 중첩 함수
함수 내부에 정의된 함수를 중첩 함수 또는 내부 함수 라 한다. 그리고 중첩함수를 포함하는 함수는 외부 함수라 부른다. 중첩 함수는 외부 함수 내부에서만 호출할 수 있다. 일반적으로 중첩 함수는 자신을 포함하는 외부 함수를 돕는 헬퍼 함수의 역할을 한다.

```
function outer(){
    let x = 1;
    //중첩 함수
    function inner(){
        let y = 2;
        //외부 함수의 변수를 참조할 수 있다.
        console.log(x+y); //3
    }
    inner();
}
outer();
```
- 호이스팅으로 인해 혼란이 발생할 수 있으므로 , if 문이나 for 문 등의 코드 블록에서 함수 선언문을 통해 함수를 정의하는 것은 바람직하지 않다.

## 콜백 함수
- 어떤 일을 반복 수행하는 repeat 함수를 정의해 보자.
```
function repeat(n){
    // i를 출력한다.
    for(let i = 0; i < n; i++){
        console.log(i);
    }
}
repeat(5); // 0,1,2,3,4
```

- repeat 함수는 매개변수를 통해 전달받은 숫자만큼 반복하며 console.log(i)를 호출한다. 만약 repeat 함수의 반복문 내부에서 다른 일을 하고 싶다면 함수를 새롭게 정의해야 한다.
```
function repeat1(n,f){
    for(let i = 0; i < n; i++){
        f(i)
    }
};

let logOdds = function(i){
    if(i%2)console.log(i)
};


repeat1(5,logOdds) // 1,3
```
이처럼 함수의 매개변수를 통해 다른 함수의 내부로 전달되는 함수를 **콜백함수** 라고 하며, 매개변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수를 **고차함수** 라고한다. 고차 함수는 매개변수를 통해 전달받은 콜백 함수의 호출 시점을 결정해서 호출한다. 콜백 함수는 고차 함수에 의해 호출되며, 이때 고차 함수는 필요에 따라 콜백 함수에 인수를 전달할 수 있다.
- 콜백함수는 함수형 프로그래밍 패러다임 뿐만 아니라 비동기 처리(이벤트 처리,Ajax 통신, 타이머 함수 등에 활용되는 중요한 패턴이다.
- 콜백 함수는 비동기 처리뿐 아니라 배열 고차 함수에서도 사용된다.

## 순수 함수와 비순수 함수
함수형 프로그래밍에서는 어떤 외부 상태에 의존하지도 않고 변경하지도 않는 즉 부수 효과가 없는 함수를 순수 함수 라 하고,외부 상태에 의존하거나 외부 상태를 변경하는, 즉 부수 효과가 있는 함수를 비순수 함수라고 한다.

- 순수함수는 동일한 인수가 전달되면 언제나 동일한 값을 반환하는 함수다.
즉, 순수 함수는 어떤 외부 상태에도 의존하지 않고 오직 매개 변수를 통해 함수 내부로 전달된 인수에게만 의존해 값을 생성해 반환한다.
- 순수 함수는 일반적으로 최소 하나 이상의 인수를 전달받는다. 
```
let count = 0;
funciton increase(n){
    return ++n
}
// 순수 함수가 반환한 결과값을 변수에 재할당 해서 상태를 변경!
count = increase(count);
console.log(count)//1

count = increase(count);
console.log(count)//2
```
반대로 함수의 외부상태에 따라 반환값이 달라지는 함수, 다시 말해 외부 상태에 의존하는 함수를 비순수 함수라고 한다.
비순수 함수의 또 하나의 특징은 순수 함수와는 달리 함수의 외부상태를 변경하는 **부수효과** 가 있다.
```
let count = 0;
function increase(){
    return ++count;
}
increase();
console.log(count); // 1

increase();
console.log(count); // 2
```
- 함수가 외부 상태를 변경하면 상태 변화를 추적하기 어려워진다. 따라서 함수 외부 상태의 변경을 지양하는 순수 함수를 사용하는 것이 좋다.
- 위 예제의 increase 함수와 같은 비순수 함수는 코드의 복잡성을 증가시킨다.
- 함수형 프로그래밍은 순수 함수와 보조 함수의 조합을 통해 외부 상태를 변경하는 부수 효과를 최소화해서 불변성을 지향하는 프로그래밍 패러다임이다.