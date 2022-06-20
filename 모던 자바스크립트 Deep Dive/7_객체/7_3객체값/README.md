# 7_3 변수

> 프로퍼티 값 갱신
```
let person = {
    name:'youngwoong'
}

person.name = 'kim'
console.log(person) // {name:'kim'}
```
- name 프로퍼티가 존재하므로 name 프로퍼티의 값이 갱신된다.

> 프로퍼티 동적 생성
- 존재하지 않는 프로퍼티에 값을 할당하면 프로퍼티가 동적으로 생성되어 추가되고 프로퍼티 값이 할당된다.

```
let person ={
    name: 'lee'
}

person.age = 20;
console.log(person);//{name:'lee' ,age:20}
```

> 프로퍼티 삭제
```
let person ={
    name: 'lee'
};
person.age = 20;
delete person.age;
console.log(person) //{name:'lee'}
```

## 객체 리터럴 확장 기능
### 프로퍼티 축약 표현

``` 
let x = 1; y =2;
const obj={
    x:x,
    y:y
};
console.log(obj) // {x:1,y:2}
```

ES6 에서는 프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일때는 **프로퍼티 키를 생략** 할수 있다.

```
let x = 1, y = 2;
const obj = {x,y}
console.log(obj) //{x:1,y:2}
```

- 프로퍼티 키를 동적 생성하려면 객체 리터럴 외부에서 대괄호 표기법을 사용해야 한다.
## 메서드 축약 표현
```
cosnt obj={
    name:'lee'
    sayHi:function(){
        console.log(`hi ${this.name}`)
    }
}
obj.sayHi(); // Hi lee
```
- 위에서 메서드를 **sayHi(){}** 식으로 작성 가능하다.
