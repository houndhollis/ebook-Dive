# 1장 변수

> 변수란 무엇인가? 왜 필요한가?

- 변수는 하나의 값을 저장하기 위해 확보한 메모리 공간 자체
- 메모리 공간을 식별하기 위해 붙인 이름을 말한다
- 프로그래밍 언어는 기억하고 싶은 값을 메모리에 저장한다.
- 저장된 값을 읽어 들여 재사용하기 위해 변수라는 메커니즘을 제공한다.
 - 변수에 값을 저장하는 것을 할당, **변수에 저장된 값을 읽어 들이는 것을 참조**

> 식별자 

- 변수 이름을 식별자 라고도 한다.
- 식별자는 어떤 값을 구별해서 식별할 수 있는 고유한 이름을 말한다.
- 식별자 용어는 변수 이름에만 국한되지 않고 함수,클래스 모두 식별자다.
- 식별자는 값이 아니라 **메모리 주소**를 기억하고 있다.

> 변수 선언이란?

- 변수 선언은 변수를 생성 하는것을 말하며, 값을 저장하기 위한 메모리 공간확보
- 변수를 선언 할때는 **let , const** 키워드를 사용한다 (ES6)
- 변수 선언이후 값을 할당하지 않았다, 따라서 변수 선언에 의해 확보된 공간은 undefined이다.

```sh
var 키워드는 여러가지 단점이 있다 var 키워드의 단점중 대표적인 것은 블록 레벨 스코프를 지원하지 않고 함수레벨 스코프를 지원한다는 것이다. 이로인해 의도치 않게 전역 변수가 선언되어 심각한 부작용이 발생한다.  let,const 가 등장한 이유 !
```

> 자바 스크립트의 엔진

- 선언단계 : 변수 이름을 등록해서 자바스크립트 엔진에 변수의 존재를 알린다.
- 초기화 단계 : 값을 저장하기 위한 메모리 공간을 확보하고 암묵적으로 undefined 를 할당해 초기화한다

var 키워드를 사용한 변수 선언은 **선언 단계와 초기화 단게가 동시에 진행된다** 

> 변수 선언의 실행 시점과 변수 호이스팅

- 자바 스크립트 코드는 인터프리터에 의해 한 줄씩 순차 적으로 실행된다
```
console.log(score) //undefined

var score; // 변수 선언문
```
- console.log 가 실행된 시점에서 참조에러는 발생하지 않고 undefined 가 출력된다
- 자바스크립트는 실행하기전에 소스코드의 평가 과정을 거치면서 소스코드 실행을 준비한다. 
- var 는 선언 단계와 초기화 단계가 소스코드가 순차적으로 실행되는 런타임 이전 단계에서 실행된다는 증거이다.

> 호이스팅

- 변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 말한다.

