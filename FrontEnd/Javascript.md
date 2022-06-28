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
#### Promise 란?
자바스크립트 비동기 처리에 사용되는 객체

### 해결안 3 ) async & await
