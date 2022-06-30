# Javascript

## 비동기 처리
참고 경로 : https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/
### 비동기 처리란?
특정 코드의 연산이 끝날 때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 특성

* ajax
* setTimeout()

### 해결안 1 ) 콜백 함수
```
function getData(callbackFunc) {
	$.get('https://domain.com/products/1', function(response) {
		callbackFunc(response); // 서버에서 받은 데이터 response를 callbackFunc() 함수에 넘겨줌
	});
}

getData(function(tableData) {
	console.log(tableData); // $.get()의 response 값이 tableData에 전달됨
});

출처 : https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/
```
```
// setTimeout 사용법.
setTimeout(()=>{
   console.log('bye')
}, 3000)

console.log('hello') // hello가 먼저 찍힌 후 3초 후 bye가 찍힌다.
```
문제점 : 콜백지옥

해결안 : Promise 또는 Async

### 해결안 2 ) Promise
참고 경로 : https://joshua1988.github.io/web-development/javascript/promise-for-beginners/
#### Promise 란?
* 자바스크립트 비동기 처리에 사용되는 객체.
* 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용.
* API를 통해 데이터를 받아오기 전에 화면에 데이터를 표시하려 하면 오류 발생 또는 빈화면이 뜸. 이를 해결하기 위함.

#### Promise 3개 상태
* Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
* Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
* Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태

#### 이행/실패 예시
```
function getData() {
  // new Promise() 추가 시 Pending 상태가 되며 resolve와 reject를 인자로 가지는 콜백함수 선언.
  return new Promise(function(resolve, reject) {
    $.get('url 주소/products/1', function(response) {
      if (response) {
        // 데이터를 받으면 resolve() 호출. Promise 이행 상태로 전환.
        resolve(response);
      }
      // Promise 실패 상태로 전환.
      reject(new Error("Request is failed"));
    });
  });
}

// 위 $.get() 호출 결과에 따라 'response' 또는 'Error' 출력
// getData()의 실행이 끝나면 호출되는 then()
getData().then(function(data) {
  // resolve()의 결과 값이 data인자로 전달됨(response 데이터가 전달됨)
  console.log(data); // response 값 출력
}).catch(function(err) {
  // reject()의 결과 값 Error를 err에 받음(catch로)
  console.error(err); // Error 출력
});

출처 : https://joshua1988.github.io/web-development/javascript/promise-for-beginners/
```

#### Promise Chaining
then() 메소드를 호출하고 나면 새로운 프로미스 객체가 리턴됨(return 있을 시만). 이를 활용하여 체이닝 가능.
```
new Promise(function(resolve, reject){
  setTimeout(function() {
    resolve(1);
  }, 2000);
})
.then(function(result) {
  console.log(result); // 1
  return result + 10;
})
.then(function(result) {
  console.log(result); // 11
  return result + 20;
})
.then(function(result) {
  console.log(result); // 31
});

출처 : https://joshua1988.github.io/web-development/javascript/promise-for-beginners/
```
API 호출 또는 setTimeout() 결과가 Promise 객체가 아닌 new Promise 결과가 Promise 객체다. 혼동X.

### 해결안 3 ) async & await
일반적으로 await의 대상이 되는 비동기 처리 코드는 Axios 등 프로미스를 반환하는 API 호출 함수.

#### async & await 예외 처리 예시
```
function fetchUser() {
  var url = 'https://jsonplaceholder.typicode.com/users/1'
  return fetch(url).then(function(response) {
    return response.json();
  });
}

function fetchTodo() {
  var url = 'https://jsonplaceholder.typicode.com/todos/1';
  return fetch(url).then(function(response) {
    return response.json();
  });
}

async function logTodoTitle() {
  try {
    var user = await fetchUser();
    if (user.id === 1) {
      var todo = await fetchTodo();
      console.log(todo.title); // delectus aut autem
    }
  } catch (error) {
    console.log(error);
  }
}

출처 : https://joshua1988.github.io/web-development/javascript/js-async-await/
```
Promise 객체를 이렇게도 받을 수 있음. (.json 붙여서)
```
async function showAvatar() {

  // JSON 읽기
  let response = await fetch('/article/promise-chaining/user.json');
  let user = await response.json();
  
  ...
  
  출처 : https://ko.javascript.info/async-await
```


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

## 함수형 프로그래밍
