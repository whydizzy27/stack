# refactor
* if 사용 시 else 사용 최소화. return 활용.

## Vue.js
### 라우팅
* a태그 href 속성을 통한 화면이동보다 $router.push 사용할 것.
* $router.push 사용함으로써 header, footer와 같은 다시 부를 필요 없는 레이아웃 컴포넌트를 재렌더링하지 않으므로 리소스 절약 가능

### addEventListener & removeEventListener
* keep-alive 대상이어도 각각 mounted, beforeDestroy 훅에 선언하는 것이 맞음.
* activated, deactivated 훅에 add/remove 를 선언하게 되면 keep-alive를 사용하는 의미가 없음.

### Browser
* 전 페이지 스크롤 위치 유지(스냅샷)는 브라우저 기능이다. keep-alive와 관련 없음.

### 함수 분리
데이터를 가져오는 용도와 가져온 데이터를 가공하는 용도를 분리하여 함수를 구현해야함.
조회와 가공을 같은 함수에서 하면 단위테스트 불가.

```
fetchBookList(){
  // 조회 API 호출 함수
  return ...
}
```
```
async getBookList(){
  // 조회 데이터 가공
  const response = await this.fetchBookList()
  this.bookList = response.bookList
}
```

### 정적 변수 관리
값 변경이 없는 변수는 data 내 선언하지 않고 import 단에 const로 선언. data에는 값 변동이 있는 변수만 적재.
```
const rowSize = 10
```

### data 내 변수 할당
* api response를 통째로 data 변수에 할당해서는 안됨. 코드 추적이 어려움. 명확하게 명시 필요.
```
this.allCnt = response.allCnt
```

### 가독성 올리기
#### 예시1
```
// 지양
this.set(this.fetchA(), this.fetchB(), ...)

// 지향
const rsltA = this.fetchA()
const rsltB = this.fetchB()

this.set(rsltA, rsltB, ...)
```

#### 예시2
```
// 지양
if( A조건 && ( B조건 || C조건 )) {

// 지향 (가독성 괜찮으면 굳이 뺄 필요 없음)
const rslt = B조건 || C조건
if( A조건 && rslt ) {
```

#### 예시3
```
// 지양
if(val === 'A' || val === 'B'){

// 지향 (대상 개수가 많아질 수록 가독성 높아짐)
if( ['A', 'B'].includes(val) ) {  // true
```

참고 경로 : https://wakestand.tistory.com/302

![image](https://user-images.githubusercontent.com/67194249/178448241-a12c5e3b-9267-4d2e-aacf-de788bda7e4c.png)
![image](https://user-images.githubusercontent.com/67194249/178448313-dd5e4bb3-b68f-4127-b7ae-c61e47b90f13.png)

some 사용 시 : 여러 값 중에 하나라도 들었을 경우를 확인하는 경우

### boolean 값 prefix
* is~
* use~
* has~
* [주의] ~Yn 은 Y/N 값이 유추되므로 boolean 값으로 사용하려면 Yn 명칭은 피해야함.

### setTimeout 대신 nextTick 활용하기
* 렌더링 후 호출되는 함수나 렌더링 시점인 mounted 훅에서 주로 사용(DOM update)
* setTimeout은 환경에 따라 시점이 달라져 불안정함.


