# 10장 스코프
> 스코프란?
- 스코프는 자바스크립트를 포함한 모든 프로그래밍 언어의 기본적이며 중요한 개념이다.
스코프의 이해가 부족하면 다른 개념을 이해하기 어려울 수 있다. 더욱이 자바스크립트의 스코프는 다른 언어의 스코프와 구별되는 특징이 있으므로 주의가 필요하다. 
- var 키워드로 선언한 변수와 let 또는 const 키워드로 선언한 변수의 스코프도 다르게 동작한다.
``` 
function add(x,y){
    console.log(x,y); // 2,5
    return x+y;
}
add(2,5)

console.log(x,y);// ReferenceError.
```
변수는 코드의 가장 바깥 영역뿐 아니라 코드 블록이나 함수 몸체 내에서도 선언할 수 있다.
- var 의 문제점에 대해서 코드를 작성 해볼려고 한다.
```
var var1 = 1;

if(true){
    var var2 = 2;
    if(true){
        var var3 = 3;;
    }
}

function foo(){
    var var4 = 4;
    function bar(){
        var var5 = 5;
    }
}

console.log(var1)// 1
console.log(var2)// 2
console.log(var3)// 3 
console.log(var4)// ReferenceError
console.log(var5)// ReferenceError
```
- var 의 경우 함수레벨 스코프에서는 걸리지만 조건문등 그냥 뚫어버리는 문제점이 발생한다.
모든 식별자는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효 범위가 결정된다. 이를 스코프라 한다. 즉 스코프는 식별자가 유효한 범위를 말한다.
- 코드가 어디서 실행되며 주변에 어떤 코드가 있는지를 **렉시컬환경** 이라고 부른다 
- 식별자는 어떤 값을 구별할 수 있어야 하므로 유일해야 한다. 따라서 식별자인 변수 이름은 중복될 수 없다. 
즉 하나의 값은 유일한 식별자에 연결 되어야 한다.
