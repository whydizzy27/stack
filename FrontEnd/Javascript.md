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

#### 이행 예시
```
function getData(callback) {
  // new Promise() 추가 시 Pending 상태가 되며 resolve와 reject를 인자로 가지는 콜백함수 선언.
  return new Promise(function(resolve, reject) {
    $.get('url 주소/products/1', function(response) {
      // 데이터를 받으면 resolve() 호출
      resolve(response);
    });
  });
}

// getData()의 실행이 끝나면 호출되는 then()
getData().then(function(tableData) {
  // resolve()의 결과 값이 여기로 전달됨(response 데이터가 전달됨)
  console.log(tableData); // $.get()의 reponse 값이 tableData에 전달됨
});

출처 : https://joshua1988.github.io/web-development/javascript/promise-for-beginners/
```
#### 실패 예시
```
function getData() {
  return new Promise(function(resolve, reject) {
    reject(new Error("Request is failed"));
  });
}

// reject()의 결과 값 Error를 err에 받음(catch로)
getData().then().catch(function(err) {
  console.log(err); // Error: Request is failed
});

```

### 해결안 3 ) async & await




## Arrow Function
