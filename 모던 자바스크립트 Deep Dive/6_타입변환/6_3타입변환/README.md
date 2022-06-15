# 6_3장 타입변환

## 단축 평가는 if 문을 대체할 수 있다.
```
let done = true
let message = '';
// if문
if(done) message = '완료';
// 단축 평가
message = done && '완료';
console.log(message) // '완료'
```

## 옵셔널 체이닝 연산자
- ES11 에서 도입된 옵셔널 체이닝 연산자 ?. 는 좌항의 피연산자가 null 또는 undefined인 경우 undefined 를 반환하고 그렇지 않으면 우항의 프로퍼티를 참조한다

```
let elem = null;
let value = elem?.value
console.log(value); // undefined
```

## null 병합 연산자
- ES11 에서 도입된 null 병합 연산자 ?? 는 좌항의 피연산자가 null 또는 undefined 인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 
반환한다. null 병합 연산자 ?? 는 변수에 기본값을 설정할 때 유용하다.

```
let foo = null ?? 'woong';
console.log(foo); // 'woong'
```

```
let foo = '' || 'default string'
console.log(foo) // 'default string'

let foo1 = '' ?? 'default string'
console.log(foo1) // 'default string'
```
