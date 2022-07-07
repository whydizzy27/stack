# Arrow Function & Hoisting

## Arrow Function
참고 경로 : https://kim-solshar.tistory.com/57
```
//es5
var add = function(a,b){
    return a+b;
}
//es6 - arrow function
const add = (a,b) => {
    return a + b;
}

//매개변수가 1개라면 소괄호도 생략할수있다.
const square = x => { return x*x };

//한줄로 작성 가능한 경우 중괄호와 return 키워드도 생략 가능하다.
const square = x => x*x;
const add = (a,b) => a+b;

//매개 변수가 없는 경우
() => { return { value : 1 }; }

//객체를 함수의 몸체와 구분해주기 위해 소괄호를 사용한다
() => ( { value : 1 } );

```

~~### Hoisting 연관부분 보완필요~~

### This

Arrow Function 내 this 전에 자바스크립트 전체적인 this 사용법 먼저 설명.

참고 경로 : https://kim-solshar.tistory.com/42

실행 문맥에 따라 다르게 동작
* 함수 실행
* 메소드(함수 내부의) 실행
* 생성자 실행
* 간접 실행


1. 함수 실행

(1) 함수와 메소드 구분
* 메소드란 객체 내부의 속성이다.
```
function hello(name) {  
  return 'Hello ' + name + '!';
}
// 함수 실행
var message = hello('World');  
console.log(message); // => 'Hello World!'
```
함수 : hello 함수 실행.

메소드 : console 객체(자바스크립트에서 제공)의 log 메소드 호출.

(2) 함수 실행에서의 this
전역객체(window)를 가리킴.

(3) 실행문맥이란?
-> 함수가 작성됐을 때가 아닌 실행될 당시의 문맥을 의미.

따라서, 실제로 함수가 실행되는 환경에서 this가 무엇을 가리킬지 고려해야함.

## Hoisting (Scope & Closure)

참고 경로 : https://kim-solshar.tistory.com/39

#### 함수 표현식과 함수 선언식
```
// 함수 표현식
var square = function(x){
    return x*x;
}
console.log(square(10)); // 100

// 함수 선언식
function add(a, b){
    return a + b;
}
console.log(add(1,2)); //3

출처: https://kim-solshar.tistory.com/57
```

#### Scope

자바스크립트의 함수 내에서 선언된 var 변수는 함수 전체를 유효한 스코프로 가짐. (함수 스코프를 따름)

let, const 는 블록 레벨 스코프이므로 아래 소스 예시로 if 블록(중괄호) 안에서만 유효함.
```
function foo() {
    if (true) {
        var color = 'blue';
    }
    console.log(color); // blue
}
foo();

출처: https://kim-solshar.tistory.com/39
```
#### Hoisting

자바스크립트 엔진은 내부에서 할당된 변수를 무조건 함수의 시작 위치로 끌어올려서 선언한다.
```
// 위 예제를 다음과 같이 처리한다.
function foo() {
    var color;

    if (true) {
        color = 'blue';
    }
    console.log(color); // blue
}
foo();

출처: https://kim-solshar.tistory.com/39
```


