# Arrow Function & Hoisting

## Arrow Function
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

출처: https://kim-solshar.tistory.com/57
```

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


